---
layout: page
title: Links
tagline: My friends.
permalink: /links.html
---


{% for f in site.data.friends %}
<div class="link-chip">
 <img alt="{{f.describe}}" src="{{f.image}}" class="link-chip-icon">
 <a title="{{f.describe}}" target="_blank" class="link-chip-title" href="{{f.url}}">{{f.name}}</a>
</div>
{% endfor %}

[返回主页](http://tommyhot.cn)
<div>
  <script src="/assets/js/aes.js"></script>
  <script src="/assets/js/mode-ecb.js"></script>
  <script>

    function getAesString(data,key){//加密
        var key = CryptoJS.enc.Utf8.parse(key);
        var data = CryptoJS.enc.Utf8.parse(data);
        var encrypted = CryptoJS.AES.encrypt(data,key,
                {
                    mode:CryptoJS.mode.ECB,
                    padding:CryptoJS.pad.Pkcs7
                });
        return encrypted.ciphertext.toString();
        // return encrypted
    }

    function getDAesString(encrypted,key){//解密
        var encrypted = CryptoJS.enc.Hex.parse(encrypted);
        encrypted = CryptoJS.enc.Base64.stringify(encrypted);
        var key  = CryptoJS.enc.Utf8.parse(key);
        var decrypted = CryptoJS.AES.decrypt(encrypted,key,
                {
                    mode:CryptoJS.mode.ECB,
                    padding:CryptoJS.pad.Pkcs7
                });
        return decrypted.toString(CryptoJS.enc.Utf8);
    }

    function getAES(){ //加密
        var data = document.getElementById("data-ipt").value;//明文
        var key  =  document.getElementById("data-pwd").value;//明文
        var encrypted = getAesString(data,key); //密文
        document.getElementById("data-out").value = encrypted;
    }

    function getDAes(){//解密
        var encrypted = document.getElementById("data-ipt").value; //密文
        var key  =  document.getElementById("data-pwd").value;//明文
        var decryptedStr = getDAesString(encrypted,key);
        document.getElementById("data-out").value = decryptedStr;
    }

    function oCopy(){
      {
				if (navigator.userAgent.match(/(iPhone|iPod|iPad);?/i)) {//区分iPhone设备
					window.getSelection().removeAllRanges();//这段代码必须放在前面否则无效
					var Url2=document.getElementById("data-out");//要复制文字的节点
					var range = document.createRange();
					// 选中需要复制的节点
					range.selectNode(Url2);
					// 执行选中元素
					window.getSelection().addRange(range);
					// 执行 copy 操作
					var successful = document.execCommand('copy');
					// 移除选中的元素
					window.getSelection().removeAllRanges();
          alert("已复制好，可贴粘。");
				}else{
					var Url2=document.getElementById("data-out");//要复制文字的节点
					Url2.select(); // 选择对象
					document.execCommand("Copy"); // 执行浏览器复制命令
          alert("已复制好，可贴粘。");
				}
      }
    }

    function clearInput() {
      var input = document.getElementById("data-ipt")
      input.value = ""
    }
    function clearPassword() {
      var pwd = document.getElementById("data-pwd")
      pwd.value = ""
    }

  </script>
  <div class="demo-wrap">
      <br>----------------华丽的分割线--------------<br>
    输入文本:<br>
    <input type="text" id="data-ipt"/>&nbsp;<button onclick="clearInput();">清除</button>
    <br/>
    输入密码:<br>
    <input type="password" id="data-pwd"/>&nbsp;<button onclick="clearPassword();">清除</button>
    <br/>
    <br/>
    <button onclick="getAES();">加密</button> 
    <button onclick="getDAes();">解密</button> 
    加密/解密后的数据:
    <br/>
    <input  id="data-out" type="text"/> 
    <button onclick="oCopy();">拷贝</button>
</div>
</div>
<hr/>

  {% if site.data.social.valine_comment.enable  == true %}
  <script src="/comment/av-min.js"></script>
  <script src="/comment/Valine.min.js"></script>
  <div id="comments"></div>
  {% include comments.html %}
  {% endif %}
  {% include scripts.html %}
