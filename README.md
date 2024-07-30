# ubuntu-keyring-hamonikr

Custom Ubuntu keyring package

- include HamoniKR Team Repo sign
- include Linuxmint sign
- include Ubuntun archive keyring
- hanla : ubuntu-keyring-2020.02.11.2
- taebaek : ubuntu-keyring-2020.02.11.4
- paektu : ubuntu-keyring_2023.11.28.1

# How to build

1) source download fro apt source
```
$ apt source linuxmint-keyring
$ gpg --import linuxmint-keyring-2022.06.21/usr/share/keyrings/linuxmint-keyring.gpg

$ apt source ubuntu-keyring
$ gpg --import ubuntu-keyring-2023.11.28.1/keyrings/ubuntu-archive-keyring.gpg 
```

2) check on local gpg key
```
gpg -k --keyid-format short
```

3) hamonikr key and linuxmint key add to ubuntu-keyring

```
cd ubuntu-keyring-2023.11.28.1/keyrings/

gpg --export \
 9EFBD28CA3E3ACE510C591F09FA298A1E42665B8 \
 302F0738F465C1535761F965A6616109451BBBF2 \
 790BC7277767219C42C86F933B4FE6ACC0B21F32 \
 843938DF228D22F7B3742BC0D94AA3F0EFE21092 \
 F6ECB3762474EDA9D21B7022871920D1991BC93C > ubuntu-archive-keyring.gpg
```

4) sha256 sum value 수정
```
cat ubuntu-archive-keyring.gpg | sha512sum > result.txt
```
result.txt 의 내용을 복사해서 상위의 패키지 루트 폴더에 있는 SHA512SUMS.txt.asc 파일안의 ubuntu-archive-keyring.gpg 해시 값을 대체
 
5) 하모니카 저장소의 키를 이용해서 재 빌드
```
sudo apt install debian-keyring 

dpkg-buildpackage -rfakeroot -m"HamoniKR <pkg@hamonikr.org>" --sign-key=9FA298A1E42665B8
```

6) 제작한 패키지 중 ubuntu-keyring*deb 파일을 ISO 이미지 안의 /pool/main/u/ubuntu-keyring 폴더에 복사
