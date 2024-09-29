# BookShoppingCartMvc (A basic e-comm system for beginners)📚🛒

## Tech stack 🧑‍💻

   - Dotnet core mvc (.Net 8)
   - MS SQLServer (Database)
   - Entity Framework Core (ORM)
   - Identity Core (Authentication)
   - Bootstrap 5 (frontend)

## Video tutorial 📺

[Youtube playlist](https://www.youtube.com/watch?v=R4ZLWD89R5w&list=PLP8UhDwXI7f_8r2Rbt7GNwf7eXZqUu_p4)

## How to run the project?🌐

I am assuming that, you have already installed **Visual Studio 2022** (It is the latest as of march,2024) and **MS SQL Server Management Studio** (I am using mssql server 2022 as of march,2024). Now, follow the following steps.

1.Open command prompt. Go to a directory where you want to clone this project. Use this command to clone the project.

```bash
git clone https://github.com/rd003/BookShoppingCart-Mvc
```

2.Go to the directory where you have cloned this project, open the directory `BookShoppingCart-Mvc`. You will find a file with name `BookShoppingCartMvc.sln`. Double click on this file and this project will be opened in Visual Studio.

3.Open `appsettings.json` file and update connection string

```json
"ConnectionStrings": {
  "conn": "data source=your_server_name;initial catalog=MovieStoreMvc; integrated security=true;encrypt=false"
}
```

4.Delete `Migrations` folder.

5.Open Tools > Package Manager > Package manager console

6.Run these 2 commands (works only with Visual studio)

```bash
  add-migration init

  update-database
```

7.Now you can run this project.

## How to register as admin and login?? 🧑‍💻🧑‍💻

1.Open the `Program.cs` file , you will find these commented lines

```c#
//using(var scope = app.Services.CreateScope())
//{
//    await DbSeeder.SeedDefaultData(scope.ServiceProvider);
//}
```

Uncomment these line and run the project. `Now stop the project and comment these lines again.`

2.Now click on login and login with these credentials.

```text
username: admin@gmail.com

password: Admin@123
```

## Data Entry 📈📉

I have provided some data of these 3 tables to test the application.

**⚠️Note: Data entry of Genre and Book is optional, you can do it from admin panel but you must enter some data for OrderStatus.**

- Genre (You can also add it from the admin panel)
- Book (You can also add it from the admin panel)
- OrderStatus (⚠️It Contain Constants. You Can not enter OrderStatus from the Admin panel. It must be added through sql server)

Please, run these scripts in a order. Genre data must be added before book.




## Other useful sql scripts

You also need to add this stored procedure in your database.

```sql
create  procedure [dbo].[Usp_GetTopNSellingBooksByDate]
@startDate datetime,@endDate datetime
as
begin

SET NOCOUNT ON;

with UnitSold as
(
select od.BookId, SUM(od.Quantity) as TotalUnitSold from [order] o 
join OrderDetail od on o.Id = od.OrderId
where o.IsPaid=1 and o.IsDeleted=0 and o.CreateDate between @startDate and @endDate
group by od.BookId
)

select top 5 b.BookName,b.AuthorName,b.[Image],us.TotalUnitSold 
from  UnitSold us
join [Book] b
on us.BookId = b.Id
order by us.TotalUnitSold desc
end
```

## Screenshots

1.Homepage

![homepage](./screenshots/1.jpg)

2.Homepage continued

![homepage2](./screenshots/2.jpg)

3.Login

![login](./screenshots/3.jpg)

4.Registration

![registration](./screenshots/4.jpg)

5.Add To Cart

![add-to-cart](./screenshots/5.jpg)

6.Cart

![cart](./screenshots/6.jpg)

7.Checkout

![cart](./screenshots/7.jpg)

8.Order success

![order_suceess](./screenshots/8_order_success.jpg)

9.Admin Login

![Admin Login](./screenshots/9_admin_login.jpg)

10.Admin Dashboard

![Admin Dashboard](./screenshots/10%20admin%20dashboard.jpg)

11.Orders

![Orders](./screenshots/11%20admin%20orders.jpg)

12.Order Detail

![Order Detail](./screenshots/12%20admin%20order%20detail.jpg)

13.Update Order Status

![Update Order Status](./screenshots/13%20Update%20Order%20Status.jpg)

14.Display Stock

![Display Stock](./screenshots/14%20%20display%20stock.jpg)

15.Update Stock

![Update Stock](./screenshots/15%20update%20stock.jpg)

16.Display Genre

![Display Genre](./screenshots/16%20display%20genres.jpg)

17.Add Genre

![Add Genre](./screenshots/17%20add%20genre.jpg)

18.Update Genre

![Update Genre](./screenshots/18%20Update%20Genre.jpg)

19.Display Books

![Display Books](./screenshots/19%20display%20books.jpg)

20.Add Book

![Add Book](./screenshots/20%20add%20books.jpg)

21.Update Book

![Update Book](./screenshots/21%20update%20book.jpg)

22.Top Selling Books

![Top Selling Books](./screenshots/22%20top%20selling%20books.jpg)



