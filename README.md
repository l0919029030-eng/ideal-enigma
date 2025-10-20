name: Build and Deploy

on:
  push:
    branches:
      - main   # 或你想要的分支

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v3

    - name: Set up Node.js
      uses: actions/setup-node@v3
      with:
        node-version: '20'

    - name: Install dependencies
      run: npm install

    - name: Build project
      run: npm run build

    # 如果要包前端/後端，可加多個 build 步驟
    # - name: Build frontend
    #   run: cd frontend && npm install && npm run build
    # - name: Build backend
    #   run: cd backend && npm install

    - name: Archive production build
      run: tar -czvf webapp.tar.gz ./dist  # 假設build結果在 dist 資料夾

    # 可加上自動部署（如 SSH/SCP 上傳、或部署到雲端），這部分可依需求補充
