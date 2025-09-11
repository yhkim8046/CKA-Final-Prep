# 인증서 내용을 텍스트로 보기
openssl x509 -in /etc/kubernetes/pki/apiserver.crt -text -noout

# 인증서 만료일 확인
openssl x509 -in /etc/kubernetes/pki/apiserver.crt -noout -enddate

# 인증서의 Subject (CN, O 등) 확인
openssl x509 -in /etc/kubernetes/pki/apiserver.crt -noout -subject
