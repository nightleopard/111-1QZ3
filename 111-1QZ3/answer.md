# 第3次隨堂-隨堂-QZ3
>
>學號：109111117 
><br />
>姓名：潘耿劭 
><br />
>作業撰寫時間：10 (mins，包含程式撰寫時間)
><br />
>最後撰寫文件日期：2022/11/14
>

本份文件包含以下主題：(至少需下面兩項，若是有多者可以自行新增)
- [x]說明內容
- [x]個人認為完成作業須具備觀念

## 說明程式與內容

指定s_City、s_Area為新字串(台北市、新北市、台中市)和
(中正區、文山區、大安區)、
(淡水區、石碇區、土城區)、
(西屯區、北屯區、東區)，指定第一個下拉式選單為上述三個其中一個，
對應下列九個選項，再指定如果rbl_Phone為空則可視值為false。
下段程式碼則為使用後結果：

```csharp
    public partial class Test : System.Web.UI.Page
    {
        string[] s_City = new string[3] { "台北市", "新北市", "台中市" };
        string[,] s_Area = new string[3, 3] {
            {"中正區", "文山區", "大安區"},
            {"淡水區", "石碇區", "土城區"},
            {"西屯區", "北屯區", "東區"}
        };
        protected void Page_Load(object sender, EventArgs e)
        {
            if (!IsPostBack)
            {
                for (int i_Ct = 0; i_Ct < s_City.Length; i_Ct++)
                {
                    ListItem a_C = new ListItem();
                    a_C.Text = a_C.Value = s_City[i_Ct];
                    dpl_City.Items.Add(a_C);
                }
            }
            if (rbl_Phone.Text == "無")
            {
                txt_Phone.Visible = false;
            }
            else
            {
                txt_Phone.Visible = true; ;
            }
        }

        protected System.Void dpl_City_SelectedIndexChanged(System.Object sender, System.EventArgs e)
        {
            mt_GenSecondList();
        }

        protected void mt_GenSecondList()
        {
            int i_ind = dpl_City.SelectedIndex;
            dpl_Area.Items.Clear();
            for (int i_Ct = 0; i_Ct < s_Area.GetLength(0); i_Ct++)
            {
                ListItem a_C = new ListItem();
                a_C.Text = a_C.Value = s_Area[i_ind, i_Ct];

                dpl_Area.Items.Add(a_C);
            }
        }
    }
```

接收Test.apex.cs的回傳偵測rbl_Phone是否為無，並顯示所回傳的資料。
下段程式碼則為使用後結果：

```csharp
    public partial class Test_Sub : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
            {
                if (Request.Form.Get("rbl_Phone") == "無")
                {
                    lb_Msg.Text = ("保單編號:") + Request.Form.Get("tb_Num") + ("<br />") + "通訊種類:" + Request.Form.Get("rbl_Phone") + ("<br />") + "所在城市:" + Request.Form.Get("dpl_City") + ("<br />") + "所在區域:" + Request.Form.Get("dpl_Area");

                }
                else
                {
                    lb_Msg.Text = ("保單編號:") + Request.Form.Get("tb_Num") + ("<br />") + "通訊種類:" + Request.Form.Get("rbl_Phone") + ("<br />") + "通訊號碼:" + Request.Form.Get("txt_Phone") + ("<br />") + "所在城市:" + Request.Form.Get("dpl_City") + ("<br />") + "所在區域:" + Request.Form.Get("dpl_Area");

                }
            }
        }
    }

```

若要於內文中標示部分.aspx檔，則使用以下標籤` ```html 程式碼 ``` `，
下段程式碼則為使用後結果：

```html
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="Test.aspx.cs" Inherits="_111_1QZ3.Test" %>

<!DOCTYPE html>

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>
    <title></title>
</head>
<body>
    <form id="form1" runat="server">
        <div>
            <h1>保單電訪記錄</h1>
            紀錄編號:<asp:TextBox ID="tb_Num" runat="server"></asp:TextBox><br />
            聯絡方式:<asp:RadioButtonList ID="rbl_Phone" runat="server" RepeatDirection="Horizontal" RepeatLayout="Flow" AutoPostBack="True">
                <asp:ListItem Text="手機" Selected="True"></asp:ListItem>
                <asp:ListItem Text="市話"></asp:ListItem>
                <asp:ListItem Text="無"></asp:ListItem>
            </asp:RadioButtonList><br />
            <asp:TextBox ID="txt_Phone" runat="server"></asp:TextBox><br /><br />
            縣市與區域:
            <asp:DropDownList ID="dpl_City" runat="server" AutoPostBack="True" OnSelectedIndexChanged="dpl_City_SelectedIndexChanged"></asp:DropDownList>
            <asp:DropDownList ID="dpl_Area" runat="server"></asp:DropDownList><br />
            <asp:Button ID="btn_Submit" runat="server" Text="送出" PostBackUrl="~/Q2_Sub.aspx" Width="80px" />
        </div>
    </form>
</body>
</html>

```

```html
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="Test_Sub.aspx.cs" Inherits="_111_1QZ3.Test_Sub" %>

<!DOCTYPE html>

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>
    <title></title>
</head>
<body>
    <form id="form1" runat="server">
        <div>
            <asp:Label ID="lb_Msg" runat="server"></asp:Label>
        </div>
    </form>
</body>
</html>
```



## 個人認為完成作業須具備觀念

要先了解物件與物件之間對應，程式碼要下在哪裡，避免程式碼下錯地方或指定代號打錯，在超連結也要用對的網頁不然開出來沒辦法跳至下一個地方。
