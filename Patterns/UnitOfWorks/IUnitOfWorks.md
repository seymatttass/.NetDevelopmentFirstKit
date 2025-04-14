* IUnitOfWorks interface örneği 

```razor
namespace School.DataAccess
{
    public interface IUnitOfWorks
    {

        IEntityRepository<TEntity> GenerateRepository<TEntity>()
        where TEntity : BaseEntity, new();
        Task BeginTransactionAsync();
        Task RollbaskTransactionAsync();
        Task CommitTransactionAsync();
    }
}

```
