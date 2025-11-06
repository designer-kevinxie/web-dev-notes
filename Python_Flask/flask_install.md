强烈建议你进行任何 Python 项目开发时，始终使用**虚拟环境 (Virtual Environment)**。

创建虚拟环境：

```bash
python3 -m venv my_project_env
```
激活虚拟环境：

```bash
source my_project_env/bin/activate
```

在虚拟环境中使用 ```pip```： 激活环境后，你就可以直接使用 ```pip``` 命令了，它只会管理当前环境下的包，不会干扰你的系统：

```bash
pip install flask
```

# 完整的 Flask 项目初始化脚本

下面我给你一份 **完整、可直接用的 Flask 项目初始化脚本**，支持自定义虚拟环境名称 👇

---

## 🧰 一键初始化脚本（macOS / Linux）

假设你要创建一个叫 `my_flask_app` 的项目，并且想把虚拟环境命名为 `env_flask`：

```bash
# 1️⃣ 创建项目文件夹
mkdir my_flask_app && cd my_flask_app

# 2️⃣ 创建自定义虚拟环境（这里是 env_flask）
python3 -m venv env_flask

# 3️⃣ 启动虚拟环境
source env_flask/bin/activate

# 4️⃣ 升级 pip
pip install --upgrade pip

# 5️⃣ 安装 Flask
pip install flask

# 6️⃣ 生成依赖文件
pip freeze > requirements.txt

# 7️⃣ 创建一个简单 Flask app
cat > app.py << 'EOF'
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello():
    return "Hello, Flask!"

if __name__ == "__main__":
    app.run(debug=True)
EOF

# 8️⃣ 运行
python app.py
```

---

## 💡 额外建议

* 如果你的项目比较大，可以建立结构：

  ```
  my_flask_app/
  ├── app/
  │   ├── __init__.py
  │   └── routes.py
  ├── env_flask/
  ├── requirements.txt
  └── run.py
  ```
* 在 `.gitignore` 里加入：

  ```
  env_flask/
  __pycache__/
  *.pyc
  ```


