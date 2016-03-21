/*
*  CopyRight for Meizu
*  notice : useFor change flash to html5
*  what can make thr video play
*  version: 0.0.10
* */

var flashPlugIn = new FlashPlugInCommon();
var s_timer;
var s_timeCount = 10;
var s_PlayerPlugIn;
var s_href;

flashPlugIn.initFlashPlugin();

function FlashPlugInCommon()
{
	this.initFlashPlugin = initFlashPlugin;
	function initFlashPlugin()
	{
		var href = document.location.href;
        s_href = href;
        console_log("console web url: " + href);
		if (href.indexOf("pptv.com") >= 0) { /* handle pptv */
			console_log("new pptv flash player . . . ");
            s_PlayerPlugIn = new PptvFlashPlugIn(href);
            s_PlayerPlugIn.handle();
		} else if (href.indexOf("youku.com") >= 0) {
			console_log("new youku flash player . . . ");
            s_PlayerPlugIn = new YoukuFlashPlugIn(href);
            s_PlayerPlugIn.handle();
		} else if (href.indexOf("iqiyi.com") >= 0) {
			console_log("new iqiyi flash player . . . ");
            s_PlayerPlugIn = new IqiyiFlashPlugIn(href);
            s_PlayerPlugIn.handle();
		} else if (href.indexOf("tudou.com") >= 0) {
			console_log("new tudou flash player . . . ");
            s_PlayerPlugIn = new TudouFlashPlugIn(href);
            s_PlayerPlugIn.handle();
		} else if (href.indexOf("qq.com") >= 0) {
            console_log("new qq flash player . . . ");
            s_PlayerPlugIn = new QqFlashPlugIn(href);
            s_PlayerPlugIn.handle();
        } else if((href.indexOf("hunantv.com") >= 0 || href.indexOf("www.mgtv.com") >= 0) && href != "www.hunantv.com") {
			console_log("hunantv web site .......");
            s_PlayerPlugIn = new HunanTvFlashPlugIn(href);
            s_PlayerPlugIn.handle();
	    } else if(href.indexOf("bilibili.com") >= 0) {
            console_log("bilibili web site .......");
            s_PlayerPlugIn = new BilibiliFlashPlugIn(href);
            s_PlayerPlugIn.handle();
        } else if(href.indexOf("sina.com.cn") >= 0) {
            console_log("sina web site .......");
            s_PlayerPlugIn = new SinaFlashPlugIn(href);
            s_PlayerPlugIn.handle();
　       } else {
            console_log("other web site .......");
            s_PlayerPlugIn = new OtherFlashPlugIn(href);
            s_PlayerPlugIn.handle();
        }
	}
}

function PptvFlashPlugIn(href)
{
	this.href = href;
	this.handle = handle;
	function handle() {
		console_log("handle pptv flash player, impli ...");
        if(document.getElementById("mz_pptv_player") != undefined)
        {
            console_log("pptv has handle before, ignore.");
            return;
        }

		var commonShareCodeNode = document.getElementById("share-input3");
		var pptvPlayerBoxNode = document.getElementById("pptv_playpage_box");
        var code = undefined;
        console_log("pptvPlayerBoxNode: -- className:" + pptvPlayerBoxNode.className + "\n style:" + pptvPlayerBoxNode.style.height);

        if(commonShareCodeNode == undefined) {
            if(webcfg != undefined) {
                code = spiltIframe(webcfg.id, "420px")
            } else {
                console_log("pptv can not handle this .");
                return ;
            }
        } else {
            code = commonShareCodeNode.value;
        }
        var pptvPlayerBoxParentNode = pptvPlayerBoxNode.parentNode;
        console_log("pptvPlayerBoxParentNode:--- className: " + pptvPlayerBoxParentNode.className + "-style:" + pptvPlayerBoxParentNode.style);
        var pptvPlayerBoxChildsNode = pptvPlayerBoxNode.childNodes;
        var childCount = pptvPlayerBoxChildsNode.length;
        for(i=0; i<childCount; i++) {
            var childNode = pptvPlayerBoxChildsNode[i];
            childNode.style.display = 'none';
            console_log("-----childNode["+ i + "]: className:" + ", tag :"  + childNode.nodeName + childNode.className + "- style:" + childNode.style);
        }

        insertNode_mz_flash("mz_pptv_player", code, pptvPlayerBoxNode, pptvPlayerBoxChildsNode[0]);
        flash2VideoCounterCallAndroid("pptv");
        console_log("code:" + code + ",add  gg pptvPlayerBoxParentNode:" + pptvPlayerBoxParentNode.ClassNames);
	}

    function spiltIframe(id, height){
        var code = "<iframe src=\"http://player.aplus.pptv.com/corporate/proxy/proxy.html#id=" + id + "\" " +
            "allowtransparency=\"true\" allowfullscreen=\"true\" allowfullscreenInteractive=\"true\" scrolling=\"no\" \t" +
            "border=\"0\" frameborder=\"0\" style=\"width:100%;height:" + height + ";\"></iframe>";
        return code;
    }
}

function YoukuFlashPlugIn(href)
{
	this.href = href;
	this.handle = handle;
	function handle() {
        console_log("handle youku flash player, impli ...");
        if(document.getElementById("mz_youku_player") != undefined)
        {
            console_log("youku has handle before, ignore.");
            return;
        }

        var commonShareCodeNode = document.getElementById("link4");
        var youkuPlayerBoxNode = document.getElementById("player");

        console_log("youkuPlayerBoxNode: -- className:" + youkuPlayerBoxNode.className + "\n style:" + youkuPlayerBoxNode.style);
        var code = commonShareCodeNode.value;
        code = code.replace("510", "\"100%\"");
        console_log("code : " + code);
        var youkuPlayerBoxParentNode = youkuPlayerBoxNode.parentNode;
        console_log("youkuPlayerBoxParentNode:--- className: " + youkuPlayerBoxParentNode.className + "-style:" + youkuPlayerBoxParentNode.style);
        var youkuPlayerBoxChilds = youkuPlayerBoxNode.childNodes;
        var childCount = youkuPlayerBoxChilds.length;
        for(i=0; i<childCount; i++) {
            var childNode = youkuPlayerBoxChilds[i];
            console_log("-----childNode["+ i + "]: className:" + ", tag :"  + childNode.nodeName + childNode.className + "- style:" + childNode.style);
        }
        youkuPlayerBoxChilds[0].style.display = 'none';
        insertNode_mz_flash("mz_youku_player", code, youkuPlayerBoxNode, youkuPlayerBoxChilds[0]);
        flash2VideoCounterCallAndroid("youku");
        console_log("code:" + code + "----->END");
	}
}

function TudouFlashPlugIn(href)
{
	this.href = href;
	this.handle = handle;
	function handle() {
        console_log("开始解析土豆网视频信息.....");
        if (document.getElementById("mz_tudou_player") != undefined) {
            console_log("tudou has handle before, ignore.");
            return;
        }

        var playerList = document.getElementsByClassName("player_container");
        var tudouPlayerBoxNode = document.getElementById("player");
        var playerBox = document.getElementsByClassName("player_box");
        var icode = pageConfig.icode;
        var vcode = pageConfig.vcode;
        if (tudouPlayerBoxNode == undefined) {
            console_log("can not find node with id = player .");
            return;
        }

        var playerListNode = undefined;

        if (playerList.length != 0) {
            playerListNode = playerList[0];
            console_log("tudou: --  tag :" + playerListNode.nodeName + "\n style:" + playerListNode.style + "\n className:" + playerListNode.className);
        }

        var width = 640;
        var height = 536;
        if(playerBox.length != 0) {
            var playerBoxNode = playerBox[0];
            width = playerBoxNode.clientWidth;
            height = playerBoxNode.clientHeight;
        } else {
            width = tudouPlayerBoxNode.clientWidth;
            height = tudouPlayerBoxNode.clientHeight;
        }

        console_log("playerBox:" + playerBox + "width:" + width + ", height:" + height);
        var code = undefined;
        if(vcode != undefined && vcode != '') {
            code = "<iframe height=" + height + " width=" + width + " src=\"http://player.youku.com/embed/" + vcode + "\" frameborder=0 allowfullscreen></iframe>";
        } else {
            code = "<iframe src=\"http://www.tudou.com/programs/view/html5embed.action?code=" + icode + "\" " +
                "allowtransparency=\"true\" allowfullscreen=\"true\" allowfullscreenInteractive=\"true\" scrolling=\"no\" \t" +
                "border=\"0\" frameborder=\"0\" style=\"width:" + width + "px;height:" + height + "px;\"></iframe>";
        }
        console_log("code : " + code + ", icode=" + icode);

        if (playerListNode != undefined) {
            var tudouPlayerBoxChilds = playerListNode.childNodes;
            var childCount = tudouPlayerBoxChilds.length;
            for (i = 0; i < childCount; i++) {
                var childNode = tudouPlayerBoxChilds[i];
                console_log("-----childNode[" + i + "]: className:" + childNode.className + ", tag :" + childNode.nodeName + "- style:" + childNode.style);
                if (childNode.nodeName.indexOf("DIV") > 0) childNode.style.display = 'none';
            }
        }

        if(playerListNode != undefined)
            tudouPlayerBoxNode.style.display = 'none';
        var noticeNode = document.getElementById("noticeWithoutFlash");
        if(noticeNode != undefined) {
            noticeNode.style.display = 'none';
            console_log("hide node with id = noticeWithoutFlash now.fdf  noticeNode:" + noticeNode.outerHTML);
            var noticeNodePar =  noticeNode.parentNode;
            noticeNodePar.removeChild(noticeNode);
        }

        console_log("hide node with id = noticeWithoutFlash in timer . playerListNode : " + playerListNode + ", tudouPlayerBoxNode:" + tudouPlayerBoxNode.outerHTML);
        if(playerListNode != undefined) {
            insertNode_mz_flash("mz_tudou_player", code, playerListNode, tudouPlayerBoxChilds[0]);
        } else {
            insertNode_mz_flash("mz_tudou_player", code, tudouPlayerBoxNode, tudouPlayerBoxNode.childNodes[0]);
        }
        flash2VideoCounterCallAndroid("tudou");
        console_log("code:" + code + "----->END");
	}
}

function IqiyiFlashPlugIn(href)
{
	this.href = href;
	this.handle = handle;
	function handle() {
        console_log("开始解析爱奇艺视频 ...");
        if(document.getElementById("mz_iqiyi_player") != undefined)
        {
            console_log("iqiyi has handle before, ignore.");
            return;
        }

        var iqiyiPlayerNode = document.getElementById("videoArea");
        var iqiyiInstallNode = document.getElementById("qiyi_flash_install");
        var flashNode = document.getElementById("flash");
        var flashboxNode = document.getElementById("flashbox");
        var needHideFlashInstall = false;

        var tvId = undefined;
        if(Q != undefined && Q.PageInfo.playPageInfo != undefined)
            tvId = Q.PageInfo.playPageInfo.tvId;

        console_log("[IqiyiFlashPlugIn]  tvId : " + tvId);
        if(iqiyiPlayerNode == undefined) {
            var videoAreaClassNode = document.getElementsByClassName("videoArea");
            if(videoAreaClassNode.length != 0) {
                iqiyiPlayerNode = videoAreaClassNode[0];
                console_log("iqiyi . can not find id=videoArea tag, ignore . get the class=videoArea instead .");
            } else {
                console_log("iqiyi . can not find id=videoArea tag . ");
                if(flashboxNode != undefined) {
                    iqiyiPlayerNode = flashboxNode;
                    tvId = flashboxNode.getAttribute("data-player-tvid");
                    console_log("iqiyi . flashboxNode handle  .tvId : " + tvId);
                    needHideFlashInstall = true;
                } else {
                    console_log("iqiyi . can not find resolve. just ignore ");
                    return;
                }
            }
        }
        if(tvId == undefined) {
            console_log("can not find tvId. return . ");
            return;
        }

        var height = iqiyiPlayerNode.clientHeight;
        if(iqiyiInstallNode != null)
            console_log("height:" + height +  ",flashboxNode=" + flashboxNode.style.height
                +  ", flashNode=" + flashNode.style.height + ",iqiyiInstallNode=" + iqiyiInstallNode.style.height);
        if(height == 0) {
            height = flashboxNode.style.height;
            if(height == 0) height = "100%";
        }

        var code = "<iframe src=\"http://open.iqiyi.com/developer/player_js/coopPlayerIndex.html?tvId=" + tvId + "\" " +
                "frameborder=\"0\" allowfullscreen=\"true\" width=\"100%\" height=\""+ height +"px\"></iframe>";
        console_log("code : " + code);

        var iqiyiPlayerBoxChilds = iqiyiPlayerNode.childNodes;
        console_log("iqiyiPlayerBoxChilds:" + iqiyiPlayerBoxChilds);
        var childCount = iqiyiPlayerBoxChilds.length;
        for(i=0; i<childCount; i++) {
            var childNode = iqiyiPlayerBoxChilds[i];
            console_log("-----childNode["+ i + "]: childNode.id:" + childNode.id + ", tag :"  + childNode.nodeName + "- className:" + childNode.className);
            if(childNode.nodeName.indexOf("DIV") >= 0) {
                childNode.style.display = 'none';
            }
        }

        if(needHideFlashInstall) {
            console_log("-------set qiyi_flash_install display none-------");
            iqiyiInstallNode.style.display = 'none';
        }

        insertNode_mz_flash("mz_iqiyi_player", code, iqiyiPlayerNode, iqiyiPlayerBoxChilds[0]);
        flash2VideoCounterCallAndroid("iqiyi");
        console_log("code:" + code + "----->END");
	}
}

function QqFlashPlugIn(href)
{
    this.href = href;
    this.handle = function() {
        console_log("[QqFlashPlugIn, handle] ------------>IN");
        if(document.getElementById("mz_qq_player") != undefined)
        {
            console_log("qq has handle before, ignore.");
            return;
        }

        this.detailHandle();
    };

    this.detailHandle = function() {
        var isMusic = false;
        var modPlayerNode = document.getElementById("mod_player");
        var concertPlayerNode = document.getElementById("concert_player");
        if(modPlayerNode == undefined) {
            console_log("[QqFlashPlugIn, timeIntervalHandle] can not find Element with id mod_player");
            if(concertPlayerNode != undefined) {
                isMusic = true;
                modPlayerNode = concertPlayerNode;
            } else {
                console_log("[QqFlashPlugIn, timeIntervalHandle] can not resolve .");
                return;
            }
        }

        var modPlayerChilds = modPlayerNode.childNodes;
        var childCount = modPlayerChilds.length;
        console_log("[QqFlashPlugIn, timeIntervalHandle] childCount : " + childCount);
        if(childCount == 0) {
            return;
        }

        /* get the video Id and auto play flag */
        var nodeInnerHtml = modPlayerChilds[0];
        var htmlStr = nodeInnerHtml.innerHTML;
        var grandSon = nodeInnerHtml.childNodes;

        console_log("[QqFlashPlugIn, timeIntervalHandle] nodeInnerHtml : " + nodeInnerHtml.nodeName + "," + nodeInnerHtml.className + ", " + nodeInnerHtml.id + "\n---:" + htmlStr);
        var posStart = htmlStr.indexOf("vid=") + "vid=".length;
        var posEnd = htmlStr.indexOf("&");
        if(posStart == undefined || posEnd == undefined) {
            console_log("[QqFlashPlugIn, findVid] can not find string .");
            return;
        }
        var vid = htmlStr.substr(posStart, posEnd - posStart);
        console_log("[QqFlashPlugIn, findVid] posStart:" + posStart + ",posEnd:" + posEnd + ", w=" + nodeInnerHtml.offsetWidth + ", height=" + nodeInnerHtml.offsetHeight + ", GrandSon=" +
            grandSon[0].offsetWidth + "," + grandSon[0].offsetHeight);

        /* new Element and append */
        var code = "<iframe frameborder=\"0\" width=100% height=100% src=\"http://v.qq.com/iframe/player.html?vid=" + vid
                    + "&tiny=0&auto=1\" allowfullscreen></iframe>";
        nodeInnerHtml.style.display = 'none';
        var newDivNode = document.createElement("DIV");
        newDivNode.style.width = '100%';
        newDivNode.style.height = '100%';
        newDivNode.id = "mz_qq_player";
        newDivNode.innerHTML = code;
        if(isMusic) {
            console_log("\n[QqFlashPlugIn, timeIntervalHandle] concertPlayerNode.parentNode : " + concertPlayerNode.parentNode.outerHTML);
            for(var i=0; i < concertPlayerNode.parentNode.childNodes.length; i++) {
                console_log("\n[QqFlashPlugIn, timeIntervalHandle] html : " + concertPlayerNode.parentNode.childNodes[i].outerHTML);
                if(concertPlayerNode.parentNode.childNodes[i].nodeName.indexOf("DIV")) {
                    console_log("[QqFlashPlugIn, timeIntervalHandle] hide node :." + concertPlayerNode.parentNode.childNodes[i].className);
                    /*concertPlayerNode.parentNode.childNodes[i].style.display = 'none';*/
                }
            }
            concertPlayerNode.parentNode.insertBefore(newDivNode, concertPlayerNode);
        } else {
            modPlayerNode.insertBefore(newDivNode, nodeInnerHtml);
        }
        flash2VideoCounterCallAndroid("qq");
        console_log("[QqFlashPlugIn, timeIntervalHandle] -------->code:" + code);
    };
}

function HunanTvFlashPlugIn(href)
{
    this.href = href;

    this.handle = function() {
        console_log("[HunanTvFlashPlugIn, handle] ------------>IN");
        console_log('开始解析芒果Tv视频地址');
        if(document.getElementById("mz_hunan_tv_player") != undefined)
        {
            console_log("hunan tv has handle before, ignore.");
            return;
        }

        var nums = s_href.match(/(\d+)/g);
        var vid = nums[nums.length - 1];
        console_log("vid　：" + vid);
        var argvs = {
            url: 'http://v.api.mgtv.com/player/video',
            jsonp: true,
            param: {
                video_id: vid
            }
        };
        ajax_mz_flash(argvs, "s_PlayerPlugIn.callbackForHunanTv");
    };

    this.callbackForHunanTv = function(argvs) {
        console_log("[callbackForHunanTv] ------>IN :" + argvs.data.stream);
        var dataStream = argvs.data.stream;
        var streamDomain = argvs.data.stream_domain;
        for(i=0 ; i < dataStream.length; i++){
            console_log("[callbackForHunanTv] dataStream[" + i + "] = " + dataStream[i].url + ", name:" + dataStream[i].name + ", streamDomain："　+ streamDomain[i]);
        }

        if(dataStream[1].url != undefined) {
            var argvs = {
                url: dataStream[1].url,
                jsonp: true,
            };
            ajax_mz_flash(argvs, "s_PlayerPlugIn.getM3u8Url");
        }
    };

    this.getM3u8Url = function(argvs) {
        console_log("[getM3u8Url] ------>IN :" + argvs.ver);
        var dataM3u8Url = argvs.info;
        console_log("[getM3u8Url] ------>IN ,dataM3u8Url " + dataM3u8Url);
        if (dataM3u8Url != undefined) {
            inplaceFlashToVideoDom(dataM3u8Url);
        }
    }

    var inplaceFlashToVideoDom = function(videoUrl) {
        if(document.getElementById("mz_hunan_tv_player") != undefined)
        {
            console_log("[inplaceFlashToVideoDom] hunan tv has handle before, ignore.");
            return;
        }

        var commonShareCodeNode = document.getElementById("player");

        console_log("[HunanTvFlashPlugIn, inplaceFlashToVideoDom] " + commonShareCodeNode.className + "\n style:" + commonShareCodeNode.style);
        var childsNode = commonShareCodeNode.childNodes;
        var childCount = childsNode.length;

        for(i=0; i<childCount; i++) {
            var childNode = childsNode[i];
            console_log("-----childNode["+ i + "]: className:" + childNode.className + ", tag :"  + childNode.nodeName + "- style:" + childNode.style + "- id:" + childNode.id);
            if(childNode.nodeName.indexOf("DIV")) {
                childNode.style.display = 'none';
            }
        }

        var newDivNode = document.createElement("DIV");
        newDivNode.id = "mz_hunan_tv_player";
        newDivNode.style.width = "100%";
        newDivNode.style.height = "100%";
        var code = "<video controls=\"controls\"  width=\"100%\" height=\"100%\" src=\""  + videoUrl + "\"></video>";
        console_log("[inplaceFlashToVideoDom] -------->code:" + code);
        newDivNode.innerHTML = code;
        commonShareCodeNode.insertBefore(newDivNode, childsNode[0]);
        flash2VideoCounterCallAndroid("mgtv");
        console_log("code:" + newDivNode.innerHTML);
    }
}


function addMzFlashJsForAjax(url, query, method, contentType, callbackName, javaScritpId) {
    if(document.getElementById(javaScritpId) != undefined)
    {
        console_log("[addMzFlashJsForAjax] bilibili add this script . . . . .");
        return false;
    }
    console_log("[addMzFlashJsForAjax]　url :" + url +  ", query : " + query + ", method : " + method + ", lll:" + query.indexOf("params="));
    var startPos = query.indexOf("params=") + "params=".length;
    if(query.indexOf("params=") < 0)
        startPos = 0;
    query = query.substr(startPos, query.length - startPos);
    url = url + "?" + query;
    console_log("[addMzFlashJsForAjax]　url :" + url + ", query : " + query + ", method : " + method + ",startPos：" + startPos);
    var innerHtmlCode = "\n init();\nfunction init() {\n" +
        "  " + "var xhr = new XMLHttpRequest();\n" +
        "  " + "var url = \"" + url + "\"; \n" +
        "  " + "var query = '';\n" +
        "  " + "xhr.open(\"" + method　+ "\", \"" + url  + "\", true);\n"+
        "  " + "xhr.setRequestHeader(\'Content-Type\', \'application\/x-www-form-urlencoded; charset=UTF-8\');\n"+
        "  " + "xhr.send();\n"+
        "  " + "xhr.onreadystatechange = function () {\n"+
        "  " + "console_log(\"xhr.readyState = \" + xhr.readyState + \" ,xhr.status = \" + xhr.status);\n "+
        "  " + "    if (xhr.readyState === 4 ) {\n"+
        "  " + "        if (xhr.status === 200) {\n"+
        "  " + "            var data = xhr.responseText;\n"+
        "  " + "        console_log(\"data :\" + data);\n " +
        "  " + "            if (\"" + contentType + "\".toLowerCase() === 'json') {\n"+
        "  " + "                try {\n"+
        "  " + "                    data = JSON.parse(data);\n"+
        "  " + "                } catch(e) {\n"+
        "  " + "                    data = -1;\n"+
        "  " + "                }\n"+
        "  " + "            }\n"+
        "  " + "        console_log(\"data :\" + data);\n " +
        "  " + "            return " + callbackName + "(data);\n"+
        "  " + "        } else {\n"+
        "  " + "            return " + callbackName + "(data);"+
        "  " + "        }\n"+
        "  " + "    }\n"+
        "  " + "} }\n";

    var scriptEle = document.createElement("script");
    scriptEle.setAttribute("type","text/javascript");
    scriptEle.setAttribute("id",javaScritpId);
    scriptEle.textContent = innerHtmlCode;
    document.body.appendChild(scriptEle);
    return true;
}

function BilibiliFlashPlugIn(href)
{
    this.href = href;
    this.handle = handle;
    function handle(href){
        console_log("[BilibiliFlashPlugIn, handle] ---------->IN , href=" + s_href);
        console_log('开始解析bilibli视频地址 .... ');
        if(document.getElementById("mz_bilibili_player") != undefined)
        {
            console_log("[inplaceFlashToVideoDom] bilibili has handle before, ignore.");
            return;
        }
        var posStart = s_href.indexOf("video/av") + "video/av".length;
        var subStrTemp = s_href.substr(posStart, s_href.length - posStart);
        var posEnd = subStrTemp.indexOf("/");
        var aid = subStrTemp.substr(0, posEnd);

        posStart = s_href.indexOf("index_") + "index_".length;
        subStrTemp = s_href.substr(posStart, s_href.length - posStart);
        posEnd = subStrTemp.indexOf(".html");
        var page = (posEnd == -1) ? 1 : subStrTemp.substr(0, posEnd);

        console_log('aid: ' + aid + ", page : " + page);
        httpProxy_mz_flash(
            'http://www.bilibili.com/m/html5',
            'get',
            {aid: aid, page: page, sid: getCookie_mz_flash('sid')},
            function (rs) {
                if (rs && rs.src) {
                    console_log("获取到<a href=\""+rs.src+"\">视频地址</a>, 并开始解析bilibli弹幕");
                } else {
                    log('解析bilibli视频地址失败', 2)
                }
            })
    };
}

function bilibiliCallback(data) {
    if(data == undefined || data.src == undefined) {
        console_log("bilibiliCallback ------------>data undfined error.");
        return;
    }
    console_log("bilibiliCallback ------------>data:" + data.src);
    inplaceFlashToVideoDom(data.src, data.cid, data.img)
}

function inplaceFlashToVideoDom(videoUrl, cid, posturl) {
    if(document.getElementById("mz_bilibili_player") != undefined)
    {
        console_log("[inplaceFlashToVideoDom] bilibili has handle before, ignore.");
        return;
    }
    console_log("[BilibiliFlashPlugIn, inplaceFlashToVideoDom]  videoUrl : " + videoUrl + ";\n cid:" + cid + ",\n posturl : " + posturl);

    var commonShareCodeNode = document.getElementById("bofqi");

    console_log("[BilibiliFlashPlugIn, inplaceFlashToVideoDom] " + commonShareCodeNode.className + "\n style:" + commonShareCodeNode.style);
    var childsNode = commonShareCodeNode.childNodes;
    var childCount = childsNode.length;

    var height = "100%";
    var width = "100%";
    console_log("[inplaceFlashToVideoDom] height : " + height + ", width : " + width);
    for(i=0; i<childCount; i++) {
        var childNode = childsNode[i];
        console_log("-----childNode["+ i + "]: className:" + childNode.className + ", tag :"  + childNode.nodeName + "- style:" + childNode.style + "- id:" + childNode.id);
        if(childNode.nodeName.indexOf("DIV") && childNode.style) {
            childNode.style.display = 'none';
        }
        if(childNode.nodeName.indexOf("OBJECT") >= 0) {
            height = childNode.height;
            width = childNode.width;
            console_log("[inplaceFlashToVideoDom] : " + height + ", width : " + width);
        }
    }

    var newDivNode = document.createElement("DIV");
    newDivNode.id = "mz_bilibili_player";
    newDivNode.style.width = "100%";
    newDivNode.style.height = "100%";
    var code = "<video controls=\"controls\"  width=" + width + " height=" + height + " src=\""  + videoUrl + "\" poster=\"" + posturl + "\"></video>";
    console_log("[inplaceFlashToVideoDom] ------>code:" + code);
    newDivNode.innerHTML = code;
    commonShareCodeNode.insertBefore(newDivNode, childsNode[0]);
    flash2VideoCounterCallAndroid("bilibili");
    console_log("code:" + newDivNode.innerHTML);
}

function SinaFlashPlugIn(href)
{
    this.href = href;
    this.handle = handle;
    function handle(href) {
        console_log("[SinaFlashPlugIn, handle] ---------->IN , href=" + s_href);
        console_log('开始解析新浪视频地址 .... ');
        var user_agent = navigator.userAgent;
        if (user_agent.indexOf("X11") < 0) {
            console_log("[SinaFlashPlugIn] not DeskTop UA, so ignore .");
            return;
        }

        if (document.getElementById("mz_sina_player") != undefined) {
            console_log("[SinaFlashPlugIn] sina has handle before, ignore.");
            return;
        }

        if (s_href.indexOf("video.sina.com.cn/l/pl/sportstv") >= 0) {
            var programId = s_href.match(/(\d+)/g);

            console_log('aid: ' + programId);
            var argvs = {
                url: 'http://s.video.sina.com.cn/live/play',
                jsonp: false,
                param: {
                    program_id: programId,
                }
            };
            ajax_mz_flash(argvs, "s_PlayerPlugIn.callbackForSina");

            return;
        }

        var videoId = undefined;
        if ($SCOPE['video'] != undefined)
            videoId = $SCOPE['video'].video_id;

        console_log("[SinaFlashPlugIn] videoId : " + videoId);
        if(videoId != undefined) {
            var argvs = {
                url: 'http://s.video.sina.com.cn/video/play',
                jsonp: true,
                param: {
                    video_id: videoId,
                }
            };
            ajax_mz_flash(argvs, "s_PlayerPlugIn.callbackForSina");

            return;
        }

    };

    this.callbackForSina = function(data) {
        console_log("[callbackForSina] ------>IN , code :" + data.code);
        var dataCode = "" + data.code;
        if (dataCode.indexOf("A0001") >= 0) {
            if(data.data.iphone != null && data.data.iphone != undefined)
                this.inplaceFlashToVideoDomForSina(data.data.iphone, "myMovieBox", "mz_sina_player");
        } else if (dataCode.indexOf("1") >= 0) {
            console_log("[callbackForSina] --ff---->IN , data.message :" + data.message);
            if(data.message.indexOf("OK") >= 0) {
                if(data.data.videos != undefined) {
                    var lengthVideos = data.data.videos.length;
                    var video = undefined;
                    for(var i = 0; i < lengthVideos; i++){
                        var videoTemp  = data.data.videos[i];
                        /*console_log("[callbackForSina] ------>IN video[" + i + "] = " + videoTemp.file_id + ", " + videoTemp.file_api);*/
                        if(videoTemp.type.indexOf("mp4") >= 0) {
                            video = videoTemp;
                        }
                    }
                    if(video != undefined) {
                        var videoUrl = video.file_api + "?vid=" + video.file_id;
                        console_log("[callbackForSina] ------>IN videoUrl:" + videoUrl );
                        this.inplaceFlashToVideoDomForSina(videoUrl, "myflashBox", "mz_sina_player");
                        s_timeCount = 10;
                        s_timer = setInterval(this.hideOrgSinaFlash, 200);
                    }
                }

            }
        } else {
            console_log("对不起，获取播放新浪视频失败,请刷新.");
        }

    };

    this.hideOrgSinaFlash = function(){
        var commonShareCodeNode = document.getElementById("myflashBox");
        console_log("[hideOrgSinaFlash] s_timer:" + s_timer + ", s_timeCount:" + s_timeCount);
        var childCount = 0;
        if(commonShareCodeNode != undefined) {
            var childsNode = commonShareCodeNode.childNodes;
            var childCount = childsNode.length;

            for(i=0; i<childCount; i++) {
                var childNode = childsNode[i];
                console_log("-----childNode["+ i + "]: className:" + childNode.className + ", tag :"  + childNode.nodeName + "- style:" + childNode.style + "- id:" + childNode.id);
                if(childNode.nodeName.indexOf("DIV") >= 0 && childNode.id.indexOf("mz_sina_player") < 0) {
                    childNode.style.display = 'none';
                }
            }
        }
        s_timeCount--;
        if(s_timeCount < 0 || childCount > 1) {
           clearInterval(s_timer);
            s_timer = -1;
        }
    }

    this.inplaceFlashToVideoDomForSina = function(videoUrl, flashId, videoId) {
        if(document.getElementById(videoId) != undefined)
        {
            console_log("该新浪视频已经处理.");
            return;
        }

        var commonShareCodeNode = document.getElementById(flashId);

        console_log("[HunanTvFlashPlugIn, inplaceFlashToVideoDom] " + commonShareCodeNode.className + "\n style:" + commonShareCodeNode.style);
        var childsNode = commonShareCodeNode.childNodes;
        var childCount = childsNode.length;

        for(i=0; i<childCount; i++) {
            var childNode = childsNode[i];
            console_log("-----childNode["+ i + "]: className:" + childNode.className + ", tag :"  + childNode.nodeName + "- style:" + childNode.style + "- id:" + childNode.id);
            if(childNode.nodeName.indexOf("DIV") >= 0) {
                childNode.style.display = 'none';
            }
        }

        var newDivNode = document.createElement("DIV");
        newDivNode.id = videoId;
        newDivNode.style.width = "100%";
        newDivNode.style.height = "100%";
        var code = "<video controls=\"controls\"  width=\"100%\" height=\"100%\" src=\""  + videoUrl + "\"></video>";
        console_log("[inplaceFlashToVideoDom] -------->code:" + code);
        newDivNode.innerHTML = code;
        commonShareCodeNode.insertBefore(newDivNode, childsNode[0]);
        flash2VideoCounterCallAndroid("sina");
        console_log("code:" + newDivNode.innerHTML);
    }
}

function addMzFlashJsForSina(url, callbackName, javaScritpId) {
    if (document.getElementById(javaScritpId) != undefined) {
        console_log("[addMzFlashJsForSina] addMzFlashJsForSina add this script . . . . .");
        return false;
    }

    console_log("[addmgtvFlashJs]　url :" + url);
    var innerHtmlCode = "getData_Mz_flash();\n" +
        " function getData_Mz_flash() {\n" +
        "      var k = \"http://video.sina.com.cn/interface/l/getMobileUrl.php?retype=jsonp&liveid=\" + $SCOPE.video.liveid;\n" +
        "      console_log(\"[addMzFlashJsForSina] k :\" + k);\n" +
        "      window.$LivePlayer.util.jsonp(k, function(a) {" +
        "         console_log(\"[addMzFlashJsForSina, handle] a.code :\" + a.data.android);\n" +
        "         " + callbackName + "(a);\n" +
        "      })\n" +
        "};"

    var scriptEle = document.createElement("script");
    scriptEle.setAttribute("type","text/javascript");
    scriptEle.setAttribute("id",javaScritpId);
    scriptEle.textContent = innerHtmlCode;
    document.body.appendChild(scriptEle);
    return true;
}

function OtherFlashPlugIn(href)
{
	this.href = href;
	this.handle = handle;
	function handle() {
        console_log("[OtherFlashPlugIn, handle] ---------->IN , href=" + s_href);
        console_log('开始解析通用视频地址。。。。。');

        var commonEmbedNode = document.getElementsByTagName("embed");
        var videoCount = commonEmbedNode.length;
        var ret = false;
        console_log('videoCount:' + videoCount);
        for(var i = 0; i < videoCount; i++)  {
            /* check the tag belone which website */
            var indexNode = commonEmbedNode[i];
            if(indexNode.style.display == 'none') {
                console_log("this node has been handled .");
                continue;
            }
            var srcCode = indexNode.src;
            console_log('srcCode:' + srcCode + ", index:" + i + ", indexNode:" + indexNode);
            if(srcCode.indexOf("player.youku.com/player.php") >= 0 && srcCode.indexOf("v.swf") >= 0) {
                ret = this.handleYoukuVideo(indexNode, srcCode, i);
            } else if(srcCode.indexOf("player.video.qiyi.com") >= 0 && srcCode.indexOf(".swf") >= 0) {
                ret = this.handleIqiyiVideo(indexNode, srcCode, i);
            } else if(srcCode.indexOf("www.tudou.com/v") >= 0 && srcCode.indexOf("v.swf") >= 0) {
                ret = this.handleTudouVideo(indexNode, srcCode, i);
            } else if(srcCode.indexOf("video.qq.com") >= 0 && srcCode.indexOf(".swf") >= 0) {
                ret = this.handleQqVideo(indexNode, srcCode, i);
            } else if(srcCode.indexOf("share.vrs.sohu.com/my/v.swf") >= 0) {
                ret = this.handleSohuVideo(indexNode, srcCode, i);
            }

            if(ret) {
                indexNode.style.display = 'none';
                console_log('hide this embed node . ');
            }

        }

	};

    this.handleYoukuVideo = function(embedNode, srcCode, index) {
        if(embedNode == undefined || srcCode == undefined || index < 0) {
            console_log('flash视频节点识别失败.');
            return false;
        }

        if(document.getElementById("mz_youku_player_" + index) != undefined)
        {
            console_log("youku has handle before, ignore.");
            return false;
        }

        var zone = this.adjustZone(embedNode);
        var height = zone.height;
        var width = zone.width;
        console_log('height:' + height + ", width:" + width);
        var posStart = srcCode.indexOf("sid/") + "sid/".length;

        var sidMid = srcCode.substr(posStart, srcCode.length - posStart);
        var posEnd = sidMid.indexOf("/");
        var sid = sidMid.substr(0, posEnd);
        if(sid.indexOf(".html", sid.length - ".html".length) >= 0) {
            sid = sid.substr(0, sid.length - ".html".length)
        }
        console_log('posStart:' + posStart + ", posEnd:" + posEnd + ", sid:" + sid + ", sidMid:" + sidMid);

        var needInsertCode = "<iframe height=" + height + " width=" + width + " src=\"http://player.youku.com/embed/" + sid + "\" frameborder=0 allowfullscreen></iframe>";

        console_log('needInsertCode:' + needInsertCode + ", s_timer:" + s_timer);
        var embedParentNode = embedNode.parentNode;
        if(href.indexOf("tieba.baidu.com") >= 0 && (s_timer == undefined || s_timer < 0)) {
            s_timeCount = 10;
            s_timer = setInterval(this.tiebaBaiduTimerFire, 200);
            console_log('setInterval tiebaBaiduTimerFire wait one seconed . s_timer: ' + s_timer);
        }
        insertNode_mz_flash("mz_youku_player_" + index, needInsertCode, embedParentNode, embedNode);
        flash2VideoCounterCallAndroid("youku");
        console_log('handleYoukuVideo finish .');
        return true;
    }

    this.handleIqiyiVideo = function(embedNode, srcCode, index) {
        if(embedNode == undefined || srcCode == undefined || index < 0) {
            console_log('flash视频节点识别失败.');
            return false;
        }

        if(document.getElementById("mz_iqiyi_player_" + index) != undefined)
        {
            console_log("iqiyi has handle before, ignore.");
            return false;
        }

        var zone = this.adjustZone(embedNode);
        var height = zone.height;
        var width = zone.width;
        console_log('height:' + height + ", width:" + width);
        var posStart = srcCode.indexOf("tvId=") + "tvId=".length;

        var tvIdMid = srcCode.substr(posStart, srcCode.length - posStart);
        var posEnd = tvIdMid.indexOf("-");
        var tvId = tvIdMid.substr(0, posEnd);
        console_log('posStart:' + posStart + ", posEnd:" + posEnd + ", sid:" + tvId + ", sidMid:" + tvIdMid);

        var needInsertCode = "<iframe src=\"http://open.iqiyi.com/developer/player_js/coopPlayerIndex.html?tvId=" + tvId + "\" " +
            "frameborder=\"0\" allowfullscreen=\"true\" width=\"" + width + "\" height=\""+ height +"px\"></iframe>";

        console_log('needInsertCode:' + needInsertCode);
        var embedParentNode = embedNode.parentNode;
        if(href.indexOf("tieba.baidu.com") >= 0 && (s_timer == undefined || s_timer < 0)) {
            s_timeCount = 10;
            s_timer = setInterval(this.tiebaBaiduTimerFire, 200);
            console_log('setInterval tiebaBaiduTimerFire wait one seconed . s_timer: ' + s_timer);
        }
        insertNode_mz_flash("mz_iqiyi_player_" + index, needInsertCode, embedParentNode, embedNode);
        flash2VideoCounterCallAndroid("iqiyi");
        console_log('handleIqiyiVideo finish .');
        return true;
    }

    this.handleTudouVideo = function(embedNode, srcCode, index) {
        if(embedNode == undefined || srcCode == undefined || index < 0) {
            console_log('flash视频节点识别失败.');
            return false;
        }

        if(document.getElementById("mz_tudou_player_" + index) != undefined)
        {
            console_log("tudou has handle before, ignore.");
            return false;
        }

        var zone = this.adjustZone(embedNode);
        var height = zone.height;
        var width = zone.width;
        console_log('height:' + height + ", width:" + width);
        var posStart = srcCode.indexOf("www.tudou.com/v/") + "www.tudou.com/v/".length;

        var icodeMid = srcCode.substr(posStart, srcCode.length - posStart);
        var posEnd = icodeMid.indexOf("/");
        var icode = icodeMid.substr(0, posEnd);
        console_log('posStart:' + posStart + ", posEnd:" + posEnd + ", sid:" + icode + ", sidMid:" + icodeMid);

        var needInsertCode = "<iframe src=\"http://www.tudou.com/programs/view/html5embed.action?code=" + icode + "\" " +
            "allowtransparency=\"true\" allowfullscreen=\"true\" allowfullscreenInteractive=\"true\" scrolling=\"no\" \t" +
            "border=\"0\" frameborder=\"0\" style=\"width:" + width + "px;height:" + height + "px;\"></iframe>";

        console_log('needInsertCode:' + needInsertCode);
        var embedParentNode = embedNode.parentNode;
        if(href.indexOf("tieba.baidu.com") >= 0 && (s_timer == undefined || s_timer < 0)) {
            s_timeCount = 10;
            s_timer = setInterval(this.tiebaBaiduTimerFire, 200);
            console_log('setInterval tiebaBaiduTimerFire wait one seconed . s_timer: ' + s_timer);
        }
        insertNode_mz_flash("mz_tudou_player_" + index, needInsertCode, embedParentNode, embedNode);
        flash2VideoCounterCallAndroid("tudou");
        console_log('handleIqiyiVideo finish .');
        return true;
    }

    this.handleQqVideo = function(embedNode, srcCode, index) {
        if(embedNode == undefined || srcCode == undefined || index < 0) {
            console_log('flash视频节点识别失败.');
            return false;
        }

        if(document.getElementById("mz_qq_player_" + index) != undefined)
        {
            console_log("qq has handle before, ignore.");
            return false;
        }

        var zone = this.adjustZone(embedNode);
        var height = zone.height;
        var width = zone.width;
        console_log('height:' + height + ", width:" + width);
        var posStart = srcCode.indexOf("vid=") + "vid=".length;

        var vidMid = srcCode.substr(posStart, srcCode.length - posStart);
        var posEnd = vidMid.indexOf("&");
        var vid = vidMid.substr(0, posEnd);
        console_log('posStart:' + posStart + ", posEnd:" + posEnd + ", vid:" + vid + ", vidMid:" + vidMid);

        var needInsertCode = "<iframe frameborder=\"0\" width=" + width + " height=" + height + " src=\"http://v.qq.com/iframe/player.html?vid=" + vid
            + "&tiny=0&auto=1\" allowfullscreen></iframe>";

        console_log('needInsertCode:' + needInsertCode);
        var embedParentNode = embedNode.parentNode;
        if(href.indexOf("tieba.baidu.com") >= 0 && (s_timer == undefined || s_timer < 0)) {
            s_timeCount = 10;
            s_timer = setInterval(this.tiebaBaiduTimerFire, 200);
            console_log('setInterval tiebaBaiduTimerFire wait one seconed . s_timer: ' + s_timer);
        }

        insertNode_mz_flash("mz_qq_player_" + index, needInsertCode, embedParentNode, embedNode);
        flash2VideoCounterCallAndroid("qq");
        console_log('qq handle finish .');
        return true;
    }

    this.handleSohuVideo = function(embedNode, srcCode, index) {
        if(embedNode == undefined || srcCode == undefined || index < 0) {
            console_log('flash视频节点识别失败.');
            return false;
        }

        if(document.getElementById("mz_sohu_player_" + index) != undefined)
        {
            console_log("sohu has handle before, ignore.");
            return false;
        }

        var zone = this.adjustZone(embedNode);
        var height = zone.height;
        var width = zone.width;
        console_log('height:' + height + ", width:" + width);
        var posStart = srcCode.indexOf("id=") + "vid=".length;

        var nidMid = srcCode.substr(posStart, srcCode.length - posStart);
        var posEnd = nidMid.indexOf("&");
        var nid = nidMid.substr(0, posEnd);
        console_log('posStart:' + posStart + ", posEnd:" + posEnd + ", nid:" + nid + ", nidMid:" + nidMid);

        var needInsertCode = "<iframe frameborder=\"0\" width=" + width + " height=" + height + " src=\"http://tv.sohu.com/upload/static/share/share_play.html#" +
            nid + "\" allowfullscreen></iframe>";

        console_log('needInsertCode:' + needInsertCode);
        var embedParentNode = embedNode.parentNode;
        if(href.indexOf("tieba.baidu.com") >= 0 && (s_timer == undefined || s_timer < 0)) {
            s_timeCount = 10;
            s_timer = setInterval(this.tiebaBaiduTimerFire, 200);
            console_log('setInterval tiebaBaiduTimerFire wait one seconed . s_timer: ' + s_timer);
        }

        insertNode_mz_flash("mz_sohu_player_" + index, needInsertCode, embedParentNode, embedNode);
        flash2VideoCounterCallAndroid("sohu");
        console_log('sohu handle finish .');
        return true;
    }

    this.tiebaBaiduTimerFire = function() {
        var isSetDisplayNone = false;
        console_log('tiebaBaiduTimerFire .......');
        var videoSrcWrapMainNodes = document.getElementsByClassName("video_src_wrap_main");
        s_timeCount--;
        console_log('videoSrcWrapMainNodes: ' + videoSrcWrapMainNodes + ", s_timeCount:" + s_timeCount + ", s_timer:" + s_timer);
        if(videoSrcWrapMainNodes != undefined) {
            console_log('videoSrcWrapMainNodes.length: ' + videoSrcWrapMainNodes.length);
            for(var i=0; i < videoSrcWrapMainNodes.length; i++) {
                videoSrcWrapMainNodes[i].style.display = 'none';
                isSetDisplayNone = true;

            }
        }
        if(isSetDisplayNone || s_timeCount == -1) {
            console_log('clearTimeout .');
            clearTimeout(s_timer);
            s_timer = -1;
        }
    }


    this.adjustZone = function (embedNode) {
        console_log("adjustZone .");
        var zone = {};
        var screenWidth = window.screen.width;
        var screenHeight = window.screen.height;
        console_log("screenWidth：" + screenWidth + ", screenHeight:" + screenHeight);
        zone.height = embedNode.height;
        zone.width = embedNode.width;
        if(screenWidth < zone.width) {
            var widthMid = screenWidth - 20;
            zone.height = widthMid * zone.height / zone.width;
            zone.width = widthMid;
        } else if (screenHeight < zone.height) {
            var heightMid = screenHeight - 20;
            zone.width = heightMid * zone.width / zone.height;
            zone.height = heightMid;
        }
        return zone;
    }
}

function insertNode_mz_flash(setId, innerHtml, parentNode, posNode) {
    var newDivNode = document.createElement("DIV");
    newDivNode.id = setId;
    newDivNode.innerHTML = innerHtml;
    parentNode.insertBefore(newDivNode, posNode);
}

/* public handle */
function defalutOption_mz_flash (option, defalutValue) {
    return option === undefined ? defalutValue : option;
}

function queryString_mz_flash (obj) {
    var query = [];
    for (one in obj) {
        if (obj.hasOwnProperty(one)) {
            query.push([one, obj[one]].join('='));
        }
    }
    return query.join('&');
}

function joinUrl_mz_flash (url, queryString) {
    if (queryString.length === 0) return url;
    return url + (url.indexOf('?') === -1 ? '?' : '&') + queryString;
}

function jsonp_mz_flash (url, callback, callbackKey, callbackName) {
    console_log("[jsonp_mz_flash] ---->url： " + url);
    var urlType = typeof(url);
    if(urlType == "object") {
        console_log("[jsonp_mz_flash] ------->not the type we need .");
        return false;
    }
    console_log("[jsonp_mz_flash] ------->urlType： " + urlType);

    callbackKey = callbackKey || 'callback';

    var script = createElement_mz_flash('script', {
        appendTo: document.body,
        src: url + (url.indexOf('?') >= 0 ? '&' : '?') + callbackKey + '=' + callbackName
    });
    console_log("[jsonp_mz_flash] -------> End ");
    return true;
}

function ajax_mz_flash (options, callbackName) {
    var url         = defalutOption_mz_flash(options.url, '');
    var callback    = defalutOption_mz_flash(options.callback, function(){});
    var context     = defalutOption_mz_flash(options.context, null);
    var query       = queryString_mz_flash(defalutOption_mz_flash(options.param, {}) );
    var method      = defalutOption_mz_flash(options.method, 'GET');
    var contentType = defalutOption_mz_flash(options.contentType, 'json');

    console_log("[ajax_mz_flash]　url :" + url + ", query=" + query + ", query : " + query + ", method : " + method);

    if (options.jsonp) {
        var ret = jsonp_mz_flash(
            joinUrl_mz_flash(url, query),
            callback.bind(context),
            typeof options.jsonp === 'string' ? options.jsonp : undefined,
            callbackName
        );
        console_log("[ajax_mz_flash] ----->ret : " + ret);
        return ret;
    }

    if(url.indexOf("www.bilibili.com") >= 0) {
        addMzFlashJsForAjax(url, query, method, contentType,　callbackName, "bilibili_javascript_id_mz");
    } else if(url.indexOf("www.mgtv.com") >= 0){
        addMzFlashJsForAjax(url, query, method, contentType, callbackName,"mgtv_javascript_id_mz");
    } else if(url.indexOf("sina.com.cn") >= 0){
        addMzFlashJsForSina(url, callbackName,"sina_javascript_id_mz");
    }

};

function createElement_mz_flash (tagName, attributes) {
    var element = document.createElement(tagName);
    if ( typeof attributes === 'function' ) {
        attributes.call(element)
    } else {
        for (var attribute in attributes) {
            if ( attributes.hasOwnProperty(attribute) ) {
                console_log("[createElement_mz_flash] ----------attribute:" + attribute + ", value:" + attributes[attribute]);
                switch (attribute) {
                    case 'appendTo':
                        attributes[attribute].appendChild(element);
                        break;
                    case 'innerHTML':
                    case 'className':
                    case 'id':
                        element[attribute] = attributes[attribute];
                        break;
                    case 'style':
                        var styles = attributes[attribute];
                        for (var name in styles)
                            if ( styles.hasOwnProperty(name) )
                                element.style[name] = styles[name];
                        break;
                    default:
                        element.setAttribute(attribute, attributes[attribute] + '');
                        break;
                }
            }
        }
    }
    return element;
}

function getCookie_mz_flash(c_name) {
    if (document.cookie.length > 0) {
        c_start = document.cookie.indexOf(c_name + "=")
        if (c_start != -1) {
            c_start = c_start + c_name.length + 1
            c_end = document.cookie.indexOf(";", c_start)
            if (c_end == -1) c_end = document.cookie.length
            return unescape(document.cookie.substring(c_start, c_end))
        }
    }
    return ""
}

function httpProxy_mz_flash (url, type, params, callback, opts) {
    opts = opts || {};
    var args = {
        url: url,
        param : {
            params: (queryString_mz_flash(params)),
            referrer: ((opts.referrer || location.href).split('#')[0]),
            post: type === 'post' ? 1 : 0,
            xml: opts.xml ? 1 : 0,
            text: opts.text ? 1 : 0,
            gzinflate: opts.gzinflate ? 1 : 0,
            ua: (opts.ua || navigator.userAgent),
        },
        jsonp: false,
        context: opts.context
    };

    ajax_mz_flash(args, "bilibiliCallback");
}

function flash2VideoCounterCallAndroid(codeSource){
    console_log("[flash2VideoCounterCallAndroid] href : " + s_href + ", codeSource : " + codeSource);
    if(MzJavascriptInterface != undefined && MzJavascriptInterface.onFlash2VideoAction != undefined) {
        MzJavascriptInterface.onFlash2VideoAction(s_href, codeSource);
    } else {
        console_log("can not call to java, no such interface .");
    }
}

function console_log(text){
    debug = true;
    if(debug){
        console.log(text);
    }
}



