# Entities

```php

    #[Entity]
    class ProfileEntity
    {

        #[Number]
        #[PrimaryKey]
        #[AutoIncrement]
        public int $id;

        #[Strings]
        public string $img;

        #[Strings]
        #[Nullable(true)]
        public string $address;

        #[DateAndTime]
        #[DefaultValue(Nexa::DATETIME_NOW)]
        public DateTime $created_at;
    }
```