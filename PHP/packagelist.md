# Create PHP Package

1. 创建并进入项目文件夹

2. 初始化 `composer init` 

3. json模板

```json
{
    "name": "itisbean/php-kkbox-api",
    "description": "kkbox open api for php",
    "type": "library",
    "keywords": ["kkbox music", "kkbox", "open api"],
    "license": "MIT",
    "authors": [
        {
            "name": "doun",
            "email": "iamdonydou@gmail.com"
        }
    ],
    "require": {
        "php": ">=5.6.0",
        "guzzlehttp/guzzle": "^6.2",
        "catfan/medoo": "^1.7"
    },
    "autoload": {
        "psr-4": {
            "kkboxMusic\\": "src/"
        }
    }
}
```

4. 本地开发，安装依赖 `composer install`

5. 关联github远程仓库，push

6. [packagist.org](https://packagist.org/packages/submit) 提交