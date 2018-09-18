# Creekdream.AspNetCore ���֮ IoC �� DI

* Ioc(���Ʒ�ת)�����������Ƴ���֮��ģ���������ϵ�����Ǵ�ͳʵ���У��ɳ������ֱ�Ӳٿء�
* DI(����ע��)������������������̬�Ľ�ĳ��������ϵע�뵽���֮�С�

��ܳ����˿��Ʒ�ת�Լ�����ע��Ľӿڣ�ʹ��IoC����Ҳ���Ա��滻�������Ŀǰ�ṩ�����ֱȽ������������Autofac��Castle.Windsor��

## ʹ�� Autofac ��ΪIoC�Լ�DI���(�Ƽ�)

1.��װ���
``` csharp
Install-Package Creekdream.Dependency.Autofac
```
2.�����������
``` csharp
public class Startup
{
    public IServiceProvider ConfigureServices(IServiceCollection services)
    {
        return services.AddCreekdream(
            options =>
            {
                options.UseAutofac();
            });
    }
}
```

## ʹ�� Castle.Windsor ��ΪIoC�Լ�DI���

1.��װ���
``` csharp
Install-Package Creekdream.Dependency.Windsor
```
2.�����������
``` csharp
public class Startup
{
    public IServiceProvider ConfigureServices(IServiceCollection services)
    {
        return services.AddCreekdream(
            options =>
            {
                options.UseWindsor();
            });
    }
}
```

## ʹ��ʾ��

``` csharp
public class UnitOfWorkManager : IUnitOfWorkManager
{
    private readonly IIocResolver _iocResolver;

    public UnitOfWorkManager(IIocResolver iocManager)
    {
        _iocResolver = iocManager;
    }
    
    public IUnitOfWorkCompleteHandle Begin(UnitOfWorkOptions options = null)
    {
        // ...
        var uow = _iocResolver.Resolve<IUnitOfWork>();
        // ...

        return uow;
    }
}
```