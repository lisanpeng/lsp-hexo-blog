---
title:  "Asp.net Ajax相关"
categories: Asp.net Ajax
tags: Asp.net Ajax
---
本文记录了在ASP.NET项目中使用Ajax的例子

<!--more-->

>Ajax调用后台方法 - 前台js

```javascript
function recoverPage() {
            var rolevalue = $("#rolevalue").val();
            var rolecode = $("#rolecode").val();

            $.ajax({
                type: "POST",
                url: "sendMsg.aspx/recoverPage",
                data: "{'rolecode':'" + rolecode + "', 'rolevalue':'" + rolevalue + "'}",
                datatype: "json",
                contentType: "application/json;charset=utf-8",
                error: function (err) {

                },
                success: function (res) {
                    $.messager.show({
                        title: '提示',
                        msg: '页面恢复消息已发送',
                        timeout: 3000,
                        showType: 'show'

                    });
                }
            });
        }
```

>Ajax调用后台方法 - 后台cs

```s
[WebMethod]
public static void recoverPage(string rolecode, string rolevalue, string user,string hostname)
{
	XmlDocument xmldoc = new XmlDocument();
    xmldoc.LoadXml(fidsXml);
	XmlNode headerNode = xmldoc.SelectSingleNode("FIDSMsg/Header");
	headerNode.SelectSingleNode("Role").InnerText = rolecode;
	headerNode.SelectSingleNode("CounterNumber").InnerText = rolevalue;
	headerNode.SelectSingleNode("MsgSendTime").InnerText = DateTime.Now.ToString("yyyy-MM-ddTHH:mm:ss");

	string[] args = new string[] { "0", xmldoc.OuterXml };
	WSHelper.InvokeWebService(url, "SendMessageToQueue", args);
}

```


>使用ajax提交表单

```javascript
$("#playAnnc").on('click', function () {
	var annctype = $("#anncType").combobox('getValue');
	var user = $("#hiddenUser").val();
	var dailyid = $("#hiddenDailyid").val();
	var hostname = $("#hiddenHostname").val();
                if (annctype != "") {
                    if (dailyid != "" ) {
                        $.ajax({
                            type: "POST",
                            url: "playAnnc.aspx?anncType=" + annctype + "&u=" + user + "&did=" + dailyid + "&gate=" + gate + "&hostname=" + hostname,
                            data: $('#formContent').serialize(),
                            datatype: "json",
                            error: function (request) {
                            },
                             success: function (data) {
                                $.messager.show({ title: '提示', msg: '消息已发送', timeout: 3000, showType: 'show' });
                            }
                        });
                    }
                }
                return false;
            });

```
