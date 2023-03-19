# qq-
这里的如获取文章标题、文章图片、logo图片地址等一些其他信息是按照本站的规则来的，使用时需要修改成自己站点的calss或id选择器来获取。如果调试不成功，可以尝试本站中的分享功能，分享时会打开新窗口，那条链接是最终要分享的，已经拼接好的参数链接，可以复制进行比对参考。
<div class="fl">分享到：</div> 
<div onclick="shareTo('qzone')">     
    <img src="http://zixuephp.net/static/images/qqzoneshare.png" width="30"> 
</div> 
<div onclick="shareTo('qq')">     
    <img src="http://zixuephp.net/static/images/qqshare.png" width="32"> 
</div> 
<div onclick="shareTo('sina')">     
    <img src="http://zixuephp.net/static/images/sinaweiboshare.png" width="36"> 
</div> 
<div onclick="shareTo('wechat')">     
    <img src="http://zixuephp.net/static/images/wechatshare.png" width="32"> 
</div>
js
function shareTo(stype){
    var ftit = '';
    var flink = '';
    var lk = '';
    //获取文章标题
    ftit = $('.pctitle').text();
    //获取网页中内容的第一张图片
    flink = $('.pcdetails img').eq(0).attr('src');
    if(typeof flink == 'undefined'){
        flink='';
    }
    //当内容中没有图片时，设置分享图片为网站logo
    if(flink == ''){
        lk = 'http://'+window.location.host+'/static/images/logo.png';
    }
    //如果是上传的图片则进行绝对路径拼接
    if(flink.indexOf('/uploads/') != -1) {
        lk = 'http://'+window.location.host+flink;
    }
    //百度编辑器自带图片获取
    if(flink.indexOf('ueditor') != -1){
        lk = flink;
    }
    //qq空间接口的传参
    if(stype=='qzone'){
        window.open('https://sns.qzone.qq.com/cgi-bin/qzshare/cgi_qzshare_onekey?url='+document.location.href+'?sharesource=qzone&title='+ftit+'&pics='+lk+'&summary='+document.querySelector('meta[name="description"]').getAttribute('content'));
    }
    //新浪微博接口的传参
    if(stype=='sina'){
        window.open('http://service.weibo.com/share/share.php?url='+document.location.href+'?sharesource=weibo&title='+ftit+'&pic='+lk+'&appkey=2706825840');
    }
    //qq好友接口的传参
    if(stype == 'qq'){
        window.open('http://connect.qq.com/widget/shareqq/index.html?url='+document.location.href+'?sharesource=qzone&title='+ftit+'&pics='+lk+'&summary='+document.querySelector('meta[name="description"]').getAttribute('content')+'&desc=php自学网，一个web开发交流的网站');
    }
    //生成二维码给微信扫描分享，php生成，也可以用jquery.qrcode.js插件实现二维码生成
    if(stype == 'wechat'){
        window.open('http://zixuephp.net/inc/qrcode_img.php?url=http://zixuephp.net/article-1.html');
    }
}
