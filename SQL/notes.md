### Useful things I've learned along the way

To reset a key/index of table to start at 1:
```sql
DBCC CHECKIDENT (‘YOUR_TABLE_NAME_HERE’, RESEED, 0)

```
