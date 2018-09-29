# Creekdream.AspNetCore ���֮ Dtoӳ��

API����MVC�Ľӿڿ��������У�ʵ��(Entity)��UI��ģ��(Dto)֮����Ҫ�໥ת������������ʹ��AutoMapper�����ģ��֮���ӳ�乤����

## ��ʼ������

��ģ������ϣ���Ȼ�����ܱ���ԭ����д���Լ����÷�ʽ��ʹ����������ƽ����

### ʹ��AutoMappe Profile����
``` csharp
/// <summary>
/// Model mapping of book entity
/// </summary>
public class BookProfile : Profile, ISingletonDependency
{
    /// <inheritdoc />
    public BookProfile(IBookService bookService)
    {
        // TODO: Use bookService do something

        CreateMap<Book, GetBookOutput>().ForMember(
            t => t.UserName,
            opts => opts.MapFrom(d => d.User.UserName)
        );
    }
}
```

### �ڿ��������
``` csharp
/// <inheritdoc />
public class Startup
{
    /// <summary>
    /// This method gets called by the runtime. Use this method to configure the HTTP request pipeline.
    /// </summary>
    public void Configure(IApplicationBuilder app, IHostingEnvironment env)
    {
        app.UseCreekdream(
            options =>
            {
                options.UseAutoMapper(
                    config =>
                    {
                        config.AddProfile(options.IocResolver.Resolve<BookProfile>());
                    });
            });
    }
}
```

### ʹ��ʾ��

#### Entity ת��Ϊ Dto
``` csharp
var books = _bookRepository.GetQueryIncluding(p => p.User).ToListAsync();
var booksOutput = books.MapTo<List<GetBookOutput>>();
```

#### Dto ת��Ϊ Entity
``` csharp
var input = new AddBookInput();
var book = input.MapTo<Book>();
book = await _bookRepository.InsertAsync(book);
```

����Ĺ���AutoMapper��ʹ�÷�ʽ����ο�[�ٷ��ĵ�](http://docs.automapper.org/en/stable/Getting-started.html)��