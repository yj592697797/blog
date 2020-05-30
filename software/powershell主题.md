##### 前置条件

- 安装[scoop](https://github.com/lukesampson/scoop)

##### 安装步骤

1. 已 **管理员** 启动`powershell`后运行

```powershell
scoop install posh-git
scoop install oh-my-posh
Install-Module posh-git
Install-Module oh-my-posh
Install-Module -Name PSReadLine -Force -SkipPublisherCheck
Install-Module Get-ChildItemColor -AllowClobber
Install-Module WindowsConsoleFonts
if (!(Test-Path -Path $PROFILE )) { New-Item -Type File -Path $PROFILE -Force }
@"
chcp 65001
Set-PSReadlineOption -EditMode Emacs
function which(`$name) { Get-Command `$name | Select-Object Definition }
function rmrf(`$item) { Remove-Item `$item -Recurse -Force }
function mkfile(`$file) { "" | Out-File `$file -Encoding ASCII }
Import-Module posh-git
Import-Module oh-my-posh
Import-Module Get-ChildItemColor
Import-Module WindowsConsoleFonts
Set-Alias l Get-ChildItemColor -option AllScope
Set-Alias ls Get-ChildItemColorFormatWide -option AllScope
Set-Theme Paradox
"@ > $PROFILE
chcp 65001
Set-PSReadlineOption -EditMode Emacs
Import-Module posh-git
Import-Module oh-my-posh
Import-Module Get-ChildItemColor
Import-Module WindowsConsoleFonts
Set-Alias l Get-ChildItemColor -option AllScope
Set-Alias ls Get-ChildItemColorFormatWide -option AllScope
Set-Theme Paradox
git clone https://gitee.com/592697797/fonts.git
cd .\fonts\
.\install.ps1
cd ..
del .\fonts\ -Recurse -Force
```

2. 在`属性`-> `字体` 中选择字体`DejaVu Sans Mono for Powerline`

##### 效果图

![](http://q81vonyew.bkt.clouddn.com/20200416105401.png)

