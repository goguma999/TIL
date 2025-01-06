**1. putty에서 root 유져로 접속**
&nbsp;

**2.centos 7의 기본 레포지토리의 url 수정**
```shell
# 수정하기 전 백업
# cp  /etc/yum.repos.d/CentOS-Base.repo  /etc/yum.repos.d/CentOS-Base.repo_backup

# vi  /etc/yum.repos.d/CentOS-Base.repo

열고 안의 내용을 전부 지워버리고 아래 내용 붙여넣기
[base]
name=CentOS-$releasever - Base
baseurl=http://vault.centos.org/7.9.2009/os/$basearch/
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
enabled=1
```
&nbsp;

**3. mariadb repo 파일 생성**
```shell
# vi /etc/yum.repos.d/MariaDB.repo

생성해서 아래 내용 붙여넣기
[mariadb] 
name = MariaDB 
baseurl = https://archive.mariadb.org/mariadb-10.3.37/yum/centos6-amd64/
gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB 
gpgcheck=1

편집종료(esc)하고 저장 후 종료(:wq!)
```
&nbsp;

**4. yum으로 mariadb 설치**
```shell
sudo yum install mariadb-server
```
&nbsp;

**5. 서버설정 파일을 설치된 설정파일로 변경**
```shell
# cp /usr/share/mysql/my-medium.cnf /etc/my.cnf
"cp: overwrite `/etc/my.cnf'? y"
```
&nbsp;

**6. UTF-8, max_allowed_packet 1G 및 테이블명 대소문자 구분안하도록 설정 추가**
```shell
# vi /etc/my.cnf

열고 [mysqld]를 찾아서 그 아래에 추가 또는 수정
[mysqld]
character-set-server=utf8
collation-server=utf8_general_ci
max_allowed_packet=1073741824
lower_case_table_names=1
```
&nbsp;

**7. mariadb 서버 시작**
```shell
# systemctl start mariadb
# mysql -u root -p   # 패스워드는 그냥 엔터
```
&nbsp;

**8. 데이터베이스 및 테이블 생성**
```sql
create database orcl;
use orcl;
```





