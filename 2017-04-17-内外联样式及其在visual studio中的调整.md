---
layout: post
title: "内外联样式及其在visual studio中的调整"
date: 2017-04-17 12:00:00 +0800
categories: 其他
tag: [asp.net,html]
---   

## visual studio中调整内联外联样式
- 按照该流程：Tools -> Options -> HTML Designer -> CSS.Change the drop downs from CSS (classes) to CSS (inline styles).

### 内联样式vs外联样式

#### 简要解释

- 内联样式：`<div style="display: none"></div>`

- 内部样式: `<style></style>`

- 外联样式：`<link href="" />`

### 详细解释

CSS 全称级联样式表 (Cascading Style Sheets)，在实际应用中，一般有以下三种级联方式。

- 1. 外联式
外联式样式表中，CSS 代码作为文件单独存放，如以 style.css 文件包含所有样式。在 HTML 中的外部级联采用 <link> 标记或者 @import 语句来引入。示例代码如下：
```
    <link rel="stylesheet" href="style.css" type="text/css" /> //link 链接
    @import url("style.css"); //@import 导入
    <link> 和 @import 的异同可参考此文：CSS 外部引用中 link 与 @import 的区别。
```
- 2. 内联式
门户网站的 CSS 代码通常采用嵌入式，即通常所说的内联方式 (Inline Style)，其使用 <style> 标记将样式定义为内部块对象。示例代码如下：

    <style type="text/css">
    <!--
    body{font-family:Arial,Helvetica,sans-serif;}
    -->
    </style>


内联 CSS 可以有效减少 HTTP 请求，提升页面性能，缓解服务器压力。由于浏览器加载完 CSS 才能渲染页面，因此能防止 CSS 文件无法读取而造成页面裸奔的现象。

- 3. 嵌入式
最初级的 CSS 写法即把代码直接添加于所修饰的标记元素。示例代码如下：

    <div style="font-family:Arial,Helvetica,sans-serif;">芒果</div>

这样做虽然更为直观，但很大程度上加大了页面体积，不符合结构与表现分离的设计思想。

总体而言，外联和内联各有优点，可综合实际情况选择适合的级联方式。

## c#中asp:Table控件

```
    <asp:Table ID="Table1" runat="server" Height="123px" Width="567px">
            <asp:TableRow runat="server">
                <asp:TableCell runat="server"></asp:TableCell>
                <asp:TableCell runat="server"></asp:TableCell>
                <asp:TableCell runat="server"></asp:TableCell>
            </asp:TableRow>
            <asp:TableRow runat="server">
                <asp:TableCell runat="server"></asp:TableCell>
                <asp:TableCell runat="server"></asp:TableCell>
                <asp:TableCell runat="server"></asp:TableCell>
            </asp:TableRow>
            <asp:TableRow runat="server">
                <asp:TableCell runat="server"></asp:TableCell>
                <asp:TableCell runat="server"></asp:TableCell>
                <asp:TableCell runat="server"></asp:TableCell>
            </asp:TableRow>
        </asp:Table>


```

对Home2.aspx的修改：

```
    <table style="margin: 0px auto;background-color:aqua;height:18px; width: 252px;">
                        <tr>
                          <td>
                              <asp:Label ID="Label1" style="text-align:center" runat="server" Text="降雨量分布图" Height="16px" Width="241px"></asp:Label>
                          </td>
                       </tr>
                    </table>
                    <table cellpadding="0" cellspacing="0">
                        <tr>
                            <td>
                            </td>
                        </tr>
                        <tr>
                            <td align="left" style="background: url(Image/切图/leftwin-mid.png);background-repeat: repeat-y">
                                开始时间：<asp:TextBox ID="DateTextBox1" runat="server" Height="16px" Width="138px"/>
                                <asp:Image ID="Image1" runat="server" ImageUrl="../Image/calendar.png" Height="24px" Width="22px" />
                                <cc1:CalendarExtender ID="CalendarExtender1" runat="server" TargetControlID="DateTextBox1" PopupButtonID="CalendarExtender1" Format="yyyy-MM-dd hh:mm:ss">
                                </cc1:CalendarExtender >
                             </td>
                        </tr>
                        <tr>
                            <td align="left" style="background: url(Image/切图/leftwin-mid.png); background-repeat: repeat-y" >
                                终止时间：<asp:TextBox ID="DateTextBox2" runat="server" Height="18px" Width="138px"  />
                                <asp:Image ID="Image2" runat="server" ImageUrl="../Image/calendar.png" Height="24px" Width="22px" />
                                <cc1:CalendarExtender ID="CalendarExtender2" runat="server" TargetControlID="DateTextBox2" PopupButtonID="CalendarExtender2" Format="yyyy-MM-dd hh:mm:ss">
                                </cc1:CalendarExtender>
                            </td>
                        </tr>
                        <tr>
                            <td style="background: url('Image/切图/leftwin-foot.png') no-repeat; height: 16px;">
                                &nbsp;
                            </td>
                        </tr>
                    </table>

```

修改为：

```
    <div style="width:260px; height:87px">
         <div style="margin: 0px auto;background-color:aqua;height:20px; width: 254px;">
             <asp:Label ID="Label1" style="text-align:center" runat="server" Text="降雨量分布图" Height="16px" Width="241px"></asp:Label>
         </div>
         <div style="width: 254px; height: 73px">
             <!--<asp:ScriptManager ID="ScriptManager1" runat="server"></asp:ScriptManager>-->
             <div style="width:258px; height:76px; margin-left: 2px;background: url('Image/切图/leftwin-foot.png') no-repeat;">
                开始时间：<asp:TextBox ID="DateTextBox1" runat="server"/>
                <asp:Image ID="Image1" runat="server" ImageUrl="../Image/calendar.png" />
                <cc1:CalendarExtender ID="CalendarExtender1" runat="server" TargetControlID="DateTextBox1" PopupButtonID="CalendarExtender1" Format="yyyy-MM-dd hh:mm:ss">
                </cc1:CalendarExtender >
                <br/>
                终止时间：<asp:TextBox ID="DateTextBox2" runat="server"  />
                <asp:Image ID="Image2" runat="server" ImageUrl="../Image/calendar.png" />
                <cc1:CalendarExtender ID="CalendarExtender2" runat="server" TargetControlID="DateTextBox2" PopupButtonID="CalendarExtender2" Format="yyyy-MM-dd hh:mm:ss">
                </cc1:CalendarExtender>
             </div>
             <div style="background: url('Image/切图/leftwin-foot.png') no-repeat; height: 16px;">
             </div>
        </div>
     </div>

```

## 检索关键词：MSDN+div

- [DIV-TABLE-CSS Layout In ASP.NET](http://www.beansoftware.com/ASP.NET-Tutorials/DIV-TABLE-CSS-Layout.aspx)

- 有趣儿的例子用以展示div在layout时的作用：
```
    <!--table-->
    <div>
        <!--tr-->
        <div style="clear:both"></div>
                <!--td-->
                <div style="float:left">
                </div>
                <!--td-->
                <div style="float:right">
                </div>
        <!--tr-->
        <div style="clear:both"></div>
                <!--td-->
                <div style="float:left">
                </div>
                <!--td-->
                <div style="float:right">
                </div>
        <!--tr-->
        <div style="clear:both"></div>
</div>
```

## 检索关键词：html client javascript error "unable to get property 'firstchild' of undefined or null reference" 

## 数据库读取到表中通用格式：
```
    
    protected void Page_Load(object sender, EventArgs e)
    {
        if (!this.IsPostBack)
        {
            this.BindGrid();
        }
    }
    private void BindGrid()
    {
        string constr = System.Configuration.ConfigurationManager.AppSettings["constr"].ToString();
        using (SqlConnection con = new SqlConnection(constr))
        {
            using (SqlCommand cmd = new SqlCommand("SELECT userName,college,department,class from tb_userinfo"))
            {
                using (SqlDataAdapter sda = new SqlDataAdapter())
                {
                    cmd.Connection = con;
                    sda.SelectCommand = cmd;
                    using (DataTable dt = new DataTable())
                    {
                        sda.Fill(dt);
                        GridView1.DataSource = dt;
                        GridView1.DataBind();
                    }
                }
            }
        }
    }

    protected void OnPageIndexChanging(object sender, GridViewPageEventArgs e)
    {
        GridView1.PageIndex = e.NewPageIndex;
        this.BindGrid();
    }
```


