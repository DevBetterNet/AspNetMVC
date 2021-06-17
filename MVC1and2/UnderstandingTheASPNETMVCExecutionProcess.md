# Cách ASP.NET 1 và 2 hoạt động

![](assets/MVC-request-life-cycle-pipeline.jpg)

Mô tả hoạt động

**Request** 

​	Chỉ với request lần đầu tiên, MVC Application sẽ chạy file Global.asasx (Global.asax.cs code behind file). Mục đích để khai báo cho ứng nhưng bị các *Route* cần cấu hình vào *RouteTable*.. Request từ lần thứ 2 trở đi sẽ chuyển qua bước tiếp theo. 

*Tham khảo*: 

Global.asax: https://docs.microsoft.com/en-us/dotnet/api/system.web.httpapplication?view=netframework-4.8

Route: https://docs.microsoft.com/en-us/dotnet/api/system.web.routing.route?view=netframework-4.8

RouteTable: https://docs.microsoft.com/en-us/dotnet/api/system.web.routing.routetable?view=netframework-4.8

**Routing**

   Mục đích sẽ tìm URL request có map với Route nào đã được khai báo ở Global.asax không ? Nếu thấy sẽ lấy cái Route đầu tiên để tạo *RequestContext*. Nếu không tìm thấy sẽ báo lỗi 404.

*Thảm khảo*

UrlRoutingModule:  https://docs.microsoft.com/en-us/dotnet/api/system.web.routing.urlroutingmodule?view=netframework-4.8

RequestContext: https://docs.microsoft.com/en-us/dotnet/api/system.web.routing.requestcontext?view=netframework-4.8



**MVC Handler**

Sẽ chọn controller để xử lý Request bằng cách tạo một đối tượng **MvcHandler** với constructor parameter chính là **RequestContext**. 

Tham khảo: https://docs.microsoft.com/en-us/dotnet/api/system.web.mvc.mvchandler?view=aspnet-mvc-5.2



**Controller**

Tạo controller: lấy thông tin từ thuộc tính MvcHandler.RequestContext để tạo controller instance.

Execute controller: sẽ gọi tới hàm Execute() này [ControllerBase Class (System.Web.Mvc) | Microsoft Docs](https://docs.microsoft.com/en-us/dotnet/api/system.web.mvc.controllerbase?view=aspnet-mvc-5.2). Đây là abstract class, sẽ gọi từ những controller mà khi phát triển ứng dụng chúng ta đã tạo.

Invoke action: ASP.NET MVC đã kết hợp ControllerActionInvoker vào Controller Base cho hầu hết các Controllers.

*Tham khảo*

DefaultControllerFactory: https://docs.microsoft.com/en-us/dotnet/api/system.web.mvc.defaultcontrollerfactory?view=aspnet-mvc-5.2



**Action Executed**

Bước này sẽ trả kết quả về cho Views thông qua một class là System.Web.Mvc.ActionResult. Ta hay gọi đây là các Result Types. 

System.Web.Mvc.ContentResult: Trả về trực tiếp giá trị.
System.Web.Mvc.EmptyResult: Nội dung trống
System.Web.Mvc.FileResult: Trả về file dữ liệu
System.Web.Mvc.HttpStatusCodeResult: Trả về HTTPStatusCode, đầu 2xxx thành công, 3xxx quyền, 4xxx lỗi phía frontend, 5xx lỗi phía backend
System.Web.Mvc.JavaScriptResult: Trả về javascript code: 
System.Web.Mvc.JsonResult: Trả về json data
System.Web.Mvc.RedirectResult: Có thể redirect tới URL khác
System.Web.Mvc.RedirectToRouteResult: Chuyển qua controller.action khác.
System.Web.Mvc.ViewResultBase  : kết hợp với View template file.

Tham khảo: [ActionResult Class (System.Web.Mvc) | Microsoft Docs](https://docs.microsoft.com/en-us/dotnet/api/system.web.mvc.actionresult?view=aspnet-mvc-5.2)





------------------------------------------



Lần đầu tiên có request tơi, MVC sẽ chạy file Global.asax. 

```C#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.Mvc;
using System.Web.Routing;

namespace MvcApplication1
{
    // Note: For instructions on enabling IIS6 or IIS7 classic mode, 
    // visit https://go.microsoft.com/?LinkId=9394801

    public class MvcApplication : System.Web.HttpApplication
    {
        public static void RegisterRoutes(RouteCollection routes)
        {
            routes.IgnoreRoute("{resource}.axd/{*pathInfo}");

            routes.MapRoute(
                "Default",                                              // Route name
                "{controller}/{action}/{id}",                           // URL with parameters
                new { controller = "Home", action = "Index", id = "" }  // Parameter defaults
            );

        }

        protected void Application_Start()
        {
            RegisterRoutes(RouteTable.Routes);
        }
    }
}
```

