# Embedded many-to-many issue

It looks like there is a breaking change between prisma `3.9.1` and `3.14.0` which results in an embedded many-to-many relation to be broken on Postgres.

## Reproduce:
```
npm install
npx prisma generate
```

## Result:
```
Prisma schema loaded from prisma/schema.prisma
Error: Schema parsing
error: Error validating: Embedded many-to-many relations are not supported on Postgres. Please use the syntax defined in https://pris.ly/d/relational-database-many-to-many
  -->  schema.prisma:14
   | 
13 |   followingUsers        User[]                  @relation("followingUsers")
14 |   followedByUsers       User[]                  @relation("followingUsers", fields: [id], references: [id])
15 | }
   | 
error: Error validating: Embedded many-to-many relations are not supported on Postgres. Please use the syntax defined in https://pris.ly/d/relational-database-many-to-many
  -->  schema.prisma:13
   | 
12 |   id                    String                  @id
13 |   followingUsers        User[]                  @relation("followingUsers")
14 |   followedByUsers       User[]                  @relation("followingUsers", fields: [id], references: [id])
   | 

Validation Error Count: 2
```
