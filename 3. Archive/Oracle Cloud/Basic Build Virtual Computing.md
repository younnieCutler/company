

---

# 📝 n8n OCI 환경 구축 기록

## 1. 오라클 계정 및 인스턴스 생성

- **OCI 계정 개설**
    
- **Compute 인스턴스 생성**
    
    - Shape: `VM.Standard.E2.1.Micro` (Always Free 대상, 1 OCPU / 1GB RAM)
    - OS: Ubuntu 22.04
    - 네트워크: VCN + 퍼블릭 서브넷
    - 퍼블릭 IP 할당
    - SSH 키 등록 (`.pem` 다운로드 → `~/.ssh/oci-key.pem`으로 이동, 권한 600)
        

---

## 2. 네트워크/보안 설정

- 인바운드 규칙 추가 (Security List 또는 NSG)
    - TCP 22 (SSH) → 내 IP
    - TCP 80 (HTTP) → 0.0.0.0/0
    - TCP 443 (HTTPS) → 0.0.0.0/0
    - TCP 5678 (n8n 테스트용) → 0.0.0.0/0
- VNIC에 올바른 보안 그룹/리스트 연결 확인
    

---

## 3. 서버 환경 세팅

- SSH 접속:
    ```bash
    ssh -i ~/.ssh/oci-key.pem ubuntu@<퍼블릭IP>
    ```
    
- 시스템 업데이트:
    ```bash
    sudo apt update && sudo apt upgrade -y
    ```
    
- Docker 설치:
    ```bash
    curl -fsSL https://get.docker.com | sh
    sudo usermod -aG docker $USER
    ```
    → 재로그인 필요
    
- Docker 테스트:
    ```bash
    sudo docker run hello-world
    ```
    

---

## 4. n8n 실행

- 볼륨 생성:
    ```bash
    sudo docker volume create n8n_data
    ```
    
- 컨테이너 실행 (도메인 없이 IP 기반):
    ```bash
    sudo docker run -d \
      --name n8n \
      --restart always \
      -p 5678:5678 \
      -e GENERIC_TIMEZONE="Asia/Tokyo" \
      -e TZ="Asia/Tokyo" \
      -e N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS=true \
      -e N8N_RUNNERS_ENABLED=true \
      -e N8N_SECURE_COOKIE=false \
      -v n8n_data:/home/node/.n8n \
      docker.n8n.io/n8nio/n8n
    ```
    
- 접속:
    ```
    http://http://141.147.160.207:5678/setup:5678
    ```

---

## 5. 운영 고려
- `--restart always` → 서버 재부팅 후 자동 실행
- 데이터는 `n8n_data` 볼륨에 저장 → 컨테이너 재생성해도 유지
- 도메인 + SSL 필요 시:
    - Nginx + Certbot 세팅 후
    - 환경변수 `N8N_HOST`, `N8N_PROTOCOL=https`, `WEBHOOK_URL` 추가
        

---

✅ 최종 상태:  
OCI Always Free Micro VM에서 **n8n 상시가동 환경 구축 완료**,  
브라우저 GUI로 업무 자동화 워크플로우 개발/운용 가능.

---