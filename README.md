# ubuntu-keyring-hamonikr

Custom Ubuntu keyring package

- include HamoniKR Team Repo sign
- include Linuxmint sign
- include Ubuntun archive keyring
- hanla : ubuntu-keyring-2020.02.11.2
- taebaek : ubuntu-keyring-2020.02.11.4

# How to build

1) source download fro apt source
```
$ apt source linuxmint-keyring
$ gpg --import linuxmint-keyring-2016.05.26/keyrings/linuxmint-keyring.gpg 

$ apt source ubuntu-keyring
$ gpg --import ubuntu-keyring-2020.02.11.2/keyrings/ubuntu-archive-keyring.gpg 
```

2) check on local gpg key
```
gpg -k --keyid-format short
```

3) hamonikr key and linuxmint key add to ubuntu-keyring

```
$ cd ubuntu-keyring-2020.02.11.2/keyrings/

gpg --export E42665B8 451BBBF2 C0B21F32 EFE21092 991BC93C > ubuntu-archive-keyring.gpg
```

4) sha256 sum value 수정
```
cat ubuntu-archive-keyring.gpg | sha512sum > result.txt
```
result.txt 의 내용을 복사해서 상위의 패키지 루트 폴더에 있는 SHA512SUMS.txt.asc 파일안의 값을 복사한 값으로 대체
 
5) 하모니카 저장소의 키를 이용해서 재 빌드
```
sudo apt install debian-keyring 

dpkg-buildpackage -rfakeroot -m"HamoniKR <pkg@hamonikr.org>" --sign-key=9FA298A1E42665B8
```

6) 제작한 패키지 중 ubuntu-keyring*deb 파일을 ISO 이미지 안의 /pool/main/u/ubuntu-keyring 폴더에 복사
