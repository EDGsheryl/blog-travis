title: NJCTF2017 线上赛 Learning Note
date: 2017-03-15 01:51:00
desc: 
tags: [CTF] 
index_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/njctf2017.jpg
banner_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/njctf2017.jpg
---

比赛的时候，只有我一个人做题
而做题的时候只做了 misc
即使 misc 只做了签到题目 QWQ

<!-- more -->

# Web

## Login

随意注册账户，进去瞟一眼，需要 admin。

利用 php 和数据库中的字段长度进行截断，注册一个 admin +（好多空格）+（杂七杂八的东西）

会覆盖 admin 的密码

然后拿刚刚注册的密码用 admin 登录就可以了

（我以为第一题就是 sqli）

## Get Flag

用 flag=XXX

F12 可以看到 cat xxx：No such file or directory

我第一反应以为是 LFI，然后就开始找目录下有什么

结果是命令执行漏洞。。。

	userinput= 1 %26 find
	或者
	userinput= 1 %26 ls /

都可以看到 flag

然后 cat $flag

## Blog

进去第一眼就看到了 Ruby。。然后马上就放弃了。。

哇。

别人的 writeup 里说直接拿源码。。。

哇。。。

源码呢QAQ

关注到 schema.rb 文件的 user 表，有一个 t.boolean "admin"

在注册的时候传入参数， user[admin]=1

之后在 /user 页面源代码找到了 flag

## Come On

随便搜一下

发现多了 ?key=1

应该是一道 sqli，宽字符注入

发现 like 没被过滤，构造 %df'||(select(hex(flag))from(flag))like(0x)%23 去模糊匹配

这时候就需要写个脚本去打完

## Chall I

前端和小姨子跑了，没办法扫描都得从头学起，干脆前后端都用 js 写吧

界面上都没有可以点的东西，唉= =

	https://www.smrrd.de/nodejs-hacking-challenge-writeup.html


还有的队伍，去 GitHub 上找 bibibibi

然后 /admin 里去登录，用纯数字去登录 N 次，大概原理是 js 的 Buffer 遇到数字参数时会将内存数据泄露出来。

payload=ximaz

从 flag 给我们的 NJCTF{P1e45e_s3arch_th1s_s0urce_cod3_0lddriver} 确实是找源代码

## Wallet

这题听说要花钱解密

源码在根目录下 /www.zip  (没做过谁知道卧槽。。。)

然后弱密码是 njctf2017...还有 php 混淆。。。

然后是 php 的弱类型 

	https://www.whitehatsec.com/blog/magic-hashes/

然后 sqli 

我后来做的时候，还去 db.php 里搞。。。是在 admin.php

id=0 不能大于0，否则就查出东西了。。

## Guess

	php://filter/convert.base64-encode/resource=

```php
<?php
error_reporting(0);
function show_error_message($message)
{
    die("<div class=\"msg error\" id=\"message\">
    <i class=\"fa fa-exclamation-triangle\"></i>$message</div>");
}

function show_message($message)
{
    echo("<div class=\"msg success\" id=\"message\">
    <i class=\"fa fa-exclamation-triangle\"></i>$message</div>");
}

function random_str($length = "32")
{
    $set = array("a", "A", "b", "B", "c", "C", "d", "D", "e", "E", "f", "F",
        "g", "G", "h", "H", "i", "I", "j", "J", "k", "K", "l", "L",
        "m", "M", "n", "N", "o", "O", "p", "P", "q", "Q", "r", "R",
        "s", "S", "t", "T", "u", "U", "v", "V", "w", "W", "x", "X",
        "y", "Y", "z", "Z", "1", "2", "3", "4", "5", "6", "7", "8", "9");
    $str = '';

    for ($i = 1; $i <= $length; ++$i) {
        $ch = mt_rand(0, count($set) - 1);
        $str .= $set[$ch];
    }

    return $str;
}

session_start();



$reg='/gif|jpg|jpeg|png/';
if (isset($_POST['submit'])) {

    $seed = rand(0,999999999);
    mt_srand($seed);
    $ss = mt_rand();
    $hash = md5(session_id() . $ss);
    setcookie('SESSI0N', $hash, time() + 3600);

    if ($_FILES["file"]["error"] > 0) {
        show_error_message("Upload ERROR. Return Code: " . $_FILES["file-upload-field"]["error"]);
    }
    $check1 = ((($_FILES["file-upload-field"]["type"] == "image/gif")
            || ($_FILES["file-upload-field"]["type"] == "image/jpeg")
            || ($_FILES["file-upload-field"]["type"] == "image/pjpeg")
            || ($_FILES["file-upload-field"]["type"] == "image/png"))
        && ($_FILES["file-upload-field"]["size"] < 204800));
    $check2=!preg_match($reg,pathinfo($_FILES['file-upload-field']['name'], PATHINFO_EXTENSION));


    if ($check2) show_error_message("Nope!");
    if ($check1) {
        $filename = './uP1O4Ds/' . random_str() . '_' . $_FILES['file-upload-field']['name'];
        if (move_uploaded_file($_FILES['file-upload-field']['tmp_name'], $filename)) {
            show_message("Upload successfully. File type:" . $_FILES["file-upload-field"]["type"]);
        } else show_error_message("Something wrong with the upload...");
    } else {
        show_error_message("only allow gif/jpeg/png files smaller than 200kb!");
    }
}
?>
```

可以把自己的 session_id 填进去 也可以干脆清空，这样就只有 $ss 了，然后就能根据 session 把 $seed 跑出来了，然后就能跑出文件目录了。

用 php 跑吧，如果用 python 跑可能跑不出来

有点怪怪的，要吃饭去上课了。。不管了

学会了 php 伪协议和一句话木马和 getshell 是什么 QWQ

## Be Admin

首先是 ./index.php.bak 源码泄露

然后是 padding oracle 攻击

鉴于没学密码学相关只是，就暂时先放一下

## Text Wall

源码泄露 ， ./.index.php.swo

ctf 的套路好多。。。web 是需要积累的。嗯。

还要知道反序列化数据

	return highlight_file('hiehiehie.txt', true).highlight_file($this->source, true);


	list="f3a6de2497f71356a3995e26a1f4f64ae48e80b1a:1:{i:0;O:8:"filelist":1:{s:6:"source";s:9:"index.php";}}"

读出 index.php，里面有 flag 的地址，再读 flag。

## Pictures' wall

我还说第一步 sqli，结果直接进去。。。

发现我们不是 root

我居然换了个 root，进去没用

看 wp，是改 header，host=127.0.0.1

然后上传图片 trick  

	<script language="php">
	system($_POST[va]);
	</script>

做题有些时候不要过于依赖浏览器，用 burp QwQ。

还有毒瘤们把 flag 删掉了！！！QAQ

## Chall 2

chall 1 的基础上

用源码搭建本地服务器，获得 admin 的 cookies

## Be Logical

504 Gateway Time-out

可能弱者不配看题吧。

# Misc

## check in

来QQ群签到啦

## Knock

是单值对应密码？？？

丢 quipqiup，然后找出对应关系，然后根据...._..._

..对应了单词_对应分割

# Reverse

100 的都看不懂

# Pwn

各位哥哥姐姐们，有 libc 嘛 QwQ

# 总结

就像学长说的，web 是需要积累的。

但是感觉并没有 ctf 留着他们的服务器，给我们看着 writeup 再次尝试。。

有点心塞。

做题的时候 总感觉好像就卡在那儿，差一点点，出来看方向不对

不会 ctf，不会开发，不会文化课，感觉啥都不会，天天混着混着，感觉越来越迷茫了。