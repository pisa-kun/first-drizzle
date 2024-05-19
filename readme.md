# typescript + drizzle

- next.js
- typescript
- drizzle
  - postgres
- docker

#### 参照
[参考文献](https://tone-row.com/blog/drizzle-orm-quickstart-tutorial-first-impressions)

## 導入手順

### pnpmでインストール
> mkdir first-drizzle  
> cd first-drizzle  

空のプロジェクトでdrizzleのインストール

> pnpm add drizzle-orm pg

> pnpm add -D @types/pg drizzle-kit typescript ts-node

※ dizzle コマンドのオプションの都合で、少し古いバージョンをインストールする
> pnpm add -D drizzle-kit@0.19.13 
> pnpm add drizzle-orm@0.28.6

設定ファイルを扱うために dotenvを追加する。
> pnpm add -D dotenv

#### docker上でpostgreの起動
> docker-compose up --build

tsconfig.jsonを作成
```json
{
    "compilerOptions": {
      "module": "CommonJS",
      "moduleResolution": "Node",
      "target": "es6",
      "jsx": "react",
      "strictNullChecks": true,
      "strictFunctionTypes": true
    },
    "exclude": ["node_modules", "**/node_modules/*"]
  }
```

package.jsonにscriptsを追加
```json
	"scripts": {
		"generate-migration": "drizzle-kit generate:pg --out src/db/migrations --schema src/db/schema.ts",
		"migrate": "ts-node src/db/migrate"
	},
```
drizzle-kitのlatest(5/20時点)だと --outオプションなどがないようなので古いバージョンのコマンドで代用

> pnpm generate-migration

作成されたマイグレートのファイルをもとに移行させる。
> pnpm migrate

.envの接続文字列は@以下をlocalhostにしておく。
> DATABASE_URL="postgresql://kotone:password@localhost:5433/mydb?schema=public"


#### 最新の参考？
https://zenn.dev/satonopan/articles/9182a9eda4d574
