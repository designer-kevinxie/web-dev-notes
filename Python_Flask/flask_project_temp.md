---
title: 标准Flask项目模板(一键脚本)
date: 2025-10-28
tags: [python,flask,VPS]
---


# 标准 Flask 项目模板(一键脚本)
**标准 Flask 项目模板**，带基础目录结构、路由、模板（HTML）、静态文件（CSS/JS），还能直接运行。


## 🧱 项目结构概览

假设你的项目叫 `my_flask_app`，虚拟环境叫 `env_flask`：

```
my_flask_app/
├── env_flask/             ← 虚拟环境（不上传到Git）
├── app/
│   ├── __init__.py        ← 初始化 Flask app
│   ├── routes.py          ← 路由控制
│   ├── static/            ← 放 CSS / JS / 图片
│   │   ├── style.css
│   └── templates/         ← 放 HTML 模板
│       └── index.html
├── run.py                 ← 启动文件
├── requirements.txt       ← 依赖
└── .gitignore
```

---

## 🧰 一键创建脚本（macOS / Linux 版）

复制以下命令在终端执行：

```bash
# 1️⃣ 创建项目文件夹
mkdir my_flask_app && cd my_flask_app

# 2️⃣ 创建虚拟环境
python3 -m venv env_flask

# 3️⃣ 启动虚拟环境
source env_flask/bin/activate

# 4️⃣ 安装 Flask
pip install flask

# 5️⃣ 生成 requirements.txt
pip freeze > requirements.txt

# 6️⃣ 创建目录结构
mkdir -p app/static app/templates

# 7️⃣ 创建 Flask 初始化文件
cat > app/__init__.py << 'EOF'
from flask import Flask

def create_app():
    app = Flask(__name__)

    from . import routes
    app.register_blueprint(routes.bp)

    return app
EOF

# 8️⃣ 创建路由文件
cat > app/routes.py << 'EOF'
from flask import Blueprint, render_template

bp = Blueprint("main", __name__)

@bp.route("/")
def index():
    return render_template("index.html", title="Home")
EOF

# 9️⃣ 创建 HTML 模板
cat > app/templates/index.html << 'EOF'
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>{{ title }}</title>
    <link rel="stylesheet" href="{{ url_for('static', filename='style.css') }}">
</head>
<body>
    <h1>Hello, Flask Project!</h1>
    <p>This is your first Flask template.</p>
</body>
</html>
EOF

# 🔟 创建 CSS 文件
cat > app/static/style.css << 'EOF'
body {
    font-family: Arial, sans-serif;
    text-align: center;
    padding-top: 50px;
}
EOF

# 11️⃣ 创建启动文件
cat > run.py << 'EOF'
from app import create_app

app = create_app()

if __name__ == "__main__":
    app.run(debug=True)
EOF

# 12️⃣ 创建 .gitignore
cat > .gitignore << 'EOF'
env_flask/
__pycache__/
*.pyc
EOF

# ✅ 运行项目
python run.py
```

---

## 🚀 启动成功后

打开浏览器访问
👉 [http://127.0.0.1:5000](http://127.0.0.1:5000)
会看到：

> “Hello, Flask Project!”

---

## 🧩 后续扩展建议

| 功能    | 文件                         | 说明                       |
| ----- | -------------------------- | ------------------------ |
| 添加新页面 | `app/routes.py`            | 增加 `@bp.route("/about")` |
| 新模板页面 | `app/templates/about.html` | 可继承 `base.html`          |
| 静态资源  | `app/static/`              | CSS, JS, 图片              |
| 环境变量  | `.env` 文件                  | 可结合 `python-dotenv` 使用   |
| 部署    | Gunicorn / Docker          | 后期可以迁移                   |


