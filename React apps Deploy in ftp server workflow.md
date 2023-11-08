name: Deploy to cPanel

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v2

    - name: Build project
      run: |
        npm install
        npm run build

    - name: Deploy to cPanel
      uses: SamKirkland/FTP-Deploy-Action@4.0.0
      with:
        server: ftp.eurohealthcare.net
        username: ${{ secrets.FTP_USERNAME }}
        password: ${{ secrets.FTP_PASSWORD }}
        server-dir: public_html/
        local-dir: ./dist/
