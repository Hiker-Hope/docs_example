Формат данных - JSON

```
{
  levels: [
    {
      id: number;
      title: "basic" | "advanced";
      locked: boolean;
      systems: [
        {
          id: number;
          title: string;
          locked: boolean;
        };
      ]
    }
  ]
}
```
