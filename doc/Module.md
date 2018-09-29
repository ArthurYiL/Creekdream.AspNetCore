# Creekdream.AspNetCore ���֮ģ�黯

����ܲο��� [ABP](https://github.com/aspnetboilerplate/aspnetboilerplate)��[OrchardCore](https://github.com/OrchardCMS/OrchardCore)��[Util](https://github.com/twitter/util)�ȿ�ܵ�ģ�黯��ơ�
* **ABP**��ͨ��ģ��������ϵִ�н�����ϲ������˳���Ⱥ�ִ�г�ʼ��������
* **Util**��ͨ��ɨ����򼯲���Ӧ�ó�������ʱ���غ��м���ģ�����ĳ��򼯲�ִ�г�ʼ������

����Ŀ�����Ƽ�������ʵ�ַ�������Ҫ���.NET CORE �µ����ģʽ��Ӧ������ģ��ĳ�ʼ�������ŵ�Startup�У�������ȷ���г���ʹ�õ�ģ�飬Ӧ�������������Ե�ִ��˳���ϵ����������������ϡ�

## ��Ŀ������չServicesBuilderOptions��������ģ�黯��ʼ��
�½�һ��ģ��,��ģ���п�ͨ��AppOptionsBuilder�е�ע�������ʼ����ģ����������
``` csharp
/// <summary>
/// ProjectName application module extension methods for <see cref="AppOptionsBuilder" />.
/// </summary>
public static class ProjectNameApplicationOptionsBuilderExtension
{
    /// <summary>
    /// Add a ProjectName application module
    /// </summary>
    public static ServicesBuilderOptions AddProjectNameApplication(this ServicesBuilderOptions builder)
    {
        builder.IocRegister.RegisterAssemblyByBasicInterface(typeof(ProjectNameApplicationOptionsBuilderExtension).Assembly);
        return builder;
    }
}
```

��ʼ��ģ�飬��Startup������������ģ��
``` csharp
/// <inheritdoc />
public class Startup
{
    /// <summary>
    /// This method gets called by the runtime. Use this method to add services to the container.
    /// For more information on how to configure your application, visit https://go.microsoft.com/fwlink/?LinkID=398940
    /// </summary>
    public IServiceProvider ConfigureServices(IServiceCollection services)
    {
        return services.AddCreekdream(
            options =>
            {
                options.AddProjectNameApplication();
            });
    }
}
```