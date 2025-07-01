# 개요

이 글은 **KDE Plasma(Wayland)** 데스크탑 환경에서 `fcitx5` 입력기의 한글 입력 방법을 설명한다. 

다음의 명령어들로 자신의 데스크탑 환경을 확인할 수 있다.

```bash 
$ echo $XDG_CURRENT_DESKTOP # KDE
$ echo $DESKTOP_SESSION # Plasma
```

 >  [Arch Linux](https://archlinux.org/)운영체제를 사용한다.
 
# Fonts

당연하게도 한글을 표시하려면 한글 글꼴이 필요하다. 여기에선 `noto-fonts-cjk` 글꼴을 사용한다.

다음 중 원하는 방법으로 시스템에 한글 글꼴을 설치하자.

## 1. 패키지 관리자를 이용하는 방법

Arch Linux 운영체제의 `pacman` 패키지 관리자를 사용하는 예제다.

```bash
$ sudo pacman -S noto-fonts-cjk
```

```bash
$ pacman -Qs noto-fonts-cjk
local/noto-fonts-cjk 20240730-1  
   Google Noto CJK fonts
```

## 2. 수동으로 설치하는 방법 

`/usr/local/share/fonts`에 원하는 폰트 파일을 설치할 수 있다.

```bash
/usr/local/share/fonts  
└── ttf
	└── noto-cjk
		├── NotoSansCJK-Light.ttc
		├── NotoSerifCJK-ExtraLight.ttc
		├── NotoSansCJK-DemiLight.ttc
		...
```

설치를 완료했다면, 다음 명령어를 사용해 폰트 캐시를 업데이트한다.

```
$ fc-cache -fv
```

>  -fv 옵션은 -f(--force), -v(--verbose) 옵션을 합친 것이다. 이 옵션을 `fc-cache` 명령어와 함께 사용하면 폰트 캐시 업데이트를 강제로, 정보를 표시하며 진행하게 된다.
# Locale

*Locale*은 사용자 인터페이스에서 사용되는 언어 및 지역, 출력 형식 등의 표준을 지정하는 문자열이다. 한글을 사용하기 위해 이 설정을 바꿔줘야 한다.
## 1. Locale  생성하기

```bash
$ /etc/locale.gen
```

위 경로에 위치한 파일의 내용 중, 다음과 같이 주석 처리된 부분을 주석 해제한다.

```bash filename="/etc/locale.gen"
# ...
#kn_IN UTF-8
#ko_KR.EUC_KR EUC-KR
ko_KR.UTF-8 UTF-8 # 주석 해제됨
#kok_IN UTF-8
#ks_IN UTF-8
# ...
```

 그리고 다음 명령어를 사용해 Locale 설정을 생성한다.
 
```bash
$ locale-gen 
Generating locales...  
 en_US.UTF-8... done  
 ko_KR.UTF-8... done  
Generation complete.
```

## 2. Locale 설정 적용하기

생성된 Locale 설정을 적용하기 위해 두 가지 중 하나를 선택한다.

### 2-1. 파일을 직접 수정하는 방법

```bash
$ /etc/locale.conf
```

위 경로에 있는 파일의 내용을 다음과 같이 설정한다. 파일이 없다면 생성한다.

```bash
LANG=ko_KR.UTF-8
```

### 2-2. 명령어를 사용하는 방법

다음 명령어를 사용해 설정을 적용할 수 있다.

```bash
$ localectl set-locale LANG=ko_KR.UTF-8
```

## 3. 설정 적용하기

2단계까지 진행했다면 다음 방법들로 설정을 적용할 수 있다.

1. 시스템 재부팅
2. 세션 로그아웃 및 로그인

또는, 다음 명령어를 통해 설정을 바로 적용할 수 있다.

```bash
$ unset LANG
$ source /etc/profile.d/locale.sh
```

그리고 다음 명령어들을 통해 사용 중인 Locale 설정을 확인할 수 있다.

- `locale` 명령어 사용 시

```bash
$ locale
LANG=ko_KR.UTF-8
LC_CTYPE="ko_KR.UTF-8"
LC_NUMERIC="ko_KR.UTF-8"
LC_TIME="ko_KR.UTF-8"
LC_COLLATE="ko_KR.UTF-8"
LC_MONETARY="ko_KR.UTF-8"
LC_MESSAGES="ko_KR.UTF-8"
LC_PAPER="ko_KR.UTF-8"
LC_NAME="ko_KR.UTF-8"
LC_ADDRESS="ko_KR.UTF-8"
LC_TELEPHONE="ko_KR.UTF-8"
LC_MEASUREMENT="ko_KR.UTF-8"
LC_IDENTIFICATION="ko_KR.UTF-8"
LC_ALL=
```

- `localectl` 명령어 사용 시

``` bash
$ localectl
System Locale: LANG=ko_KR.UTF-8
    VC Keymap: us
	X11 Layout: us
    X11 Model: pc105+inet
	X11 Options: terminate:ctrl_alt_bksp
```

- `echo $LANG` 사용 시

```bash
$ echo $LANG
ko_KR.UTF-8
```

> [!INFO]
> 위의 설정이 정상적으로 적용되었는데도 시스템 설정 패널 등 일부 창에 한글이 적용되지 않는 문제가 발생할 수 있다. 이 경우 `~/.config/plasma-localerc` 파일의 내용을 다음과 같이 변경한다.
> ``` 
> [Format]
> LANG=ko_KR.UTF-8
> ```

# fcitx5

## 패키지 설치

패키지 관리자를 이용해 [`fcitx5`](https://fcitx-im.org/wiki/Fcitx_5) 한글 입력기를 설치한다.

```bash
$ sudo pacman -S fcitx5-hangul
```

> [!WARNING]
> 2025년 현재 `fcitx5`는 `GNOME`과의 호환성이 떨어지므로 

