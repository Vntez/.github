Ở mỗi repo dự án, bạn chỉ cần một file rất ngắn (.github/workflows/deploy.yml) để gọi lại workflow chuẩn đó, truyền tham số thư mục đích và tên PM2.

```yml
name: Deploy
on:
  push:
    branches: [ main ]
jobs:
  call:
    uses: Vntez/.github/.github/workflows/nest-pm2.yml@main
    with:
      app_path: /srv/apps/<name-services>
      pm2_name: <name-services>
```

// /srv/apps/auth-api/ecosystem.config.js
```js
module.exports = {
  apps: [{
    name: "<name-services>",
    script: "dist/main.js",
    exec_mode: "fork",
    instances: 1,
    env: { NODE_ENV: "production", PORT: 3101 }
  }]
};
```

File yêu cầu trong github
- dist/
- ecosystem.config.js
- .env