# 自定义OpenAI兼容API配置指南

## 快速开始

只需在 `.env` 文件中添加自定义配置即可使用OpenAI兼容的API服务。

## 配置方法

### 方法1：统一配置（使用同一个API服务）

在 `.env` 文件中设置：
```bash
# 使用相同的API服务
OPENAI_API_KEY=your_api_key_here
OPENAI_BASE_URL=https://your-api-service.com/v1
```

### 方法2：分别配置（embedding和generator使用不同服务）

在 `.env` 文件中设置：
```bash
# Embedding模型配置
EMBEDDING_API_KEY=your_embedding_api_key
EMBEDDING_BASE_URL=https://your-embedding-api.com/v1
EMBEDDING_MODEL_NAME=text-embedding-3-small

# Generator模型配置
GENERATOR_API_KEY=your_generator_api_key
GENERATOR_BASE_URL=https://your-generator-api.com/v1
GENERATOR_MODEL_NAME=gpt-3.5-turbo
```

## 常用服务配置示例

### 1. 阿里巴巴DashScope (通义千问)
```bash
# Embedding
EMBEDDING_API_KEY=your_dashscope_key
EMBEDDING_BASE_URL=https://dashscope.aliyuncs.com/compatible-mode/v1
EMBEDDING_MODEL_NAME=text-embedding-v3

# Generator
GENERATOR_API_KEY=your_dashscope_key
GENERATOR_BASE_URL=https://dashscope.aliyuncs.com/compatible-mode/v1
GENERATOR_MODEL_NAME=qwen-plus
```

### 2. 本地Ollama
```bash
# Embedding
EMBEDDING_API_KEY=ollama
EMBEDDING_BASE_URL=http://localhost:11434/v1
EMBEDDING_MODEL_NAME=nomic-embed-text

# Generator
GENERATOR_API_KEY=ollama
GENERATOR_BASE_URL=http://localhost:11434/v1
GENERATOR_MODEL_NAME=llama3:8b
```

### 3. Moonshot AI
```bash
# Generator
GENERATOR_API_KEY=your_moonshot_key
GENERATOR_BASE_URL=https://api.moonshot.cn/v1
GENERATOR_MODEL_NAME=moonshot-v1-8k
```

### 4. 通义千问API
```bash
# Generator
GENERATOR_API_KEY=your_qwen_key
GENERATOR_BASE_URL=https://dashscope.aliyuncs.com/compatible-mode/v1
GENERATOR_MODEL_NAME=qwen-plus
```

### 5. 零一万物
```bash
# Generator
GENERATOR_API_KEY=your_yi_key
GENERATOR_BASE_URL=https://api.lingyiwanwu.com/v1
GENERATOR_MODEL_NAME=yi-large
```

## 优先级说明

1. **自定义配置优先**：如果设置了 `EMBEDDING_*` 和 `GENERATOR_*` 变量，将使用这些配置
2. **回退到OPENAI配置**：如果未设置自定义配置，将使用 `OPENAI_*` 变量
3. **使用默认值**：如果都未设置，将使用OpenAI官方配置

## 验证配置

启动服务后，系统会自动检测并使用配置。你可以通过以下方式验证：

1. 检查启动日志中的API配置信息
2. 测试生成Wiki功能是否正常
3. 检查API调用是否成功

## 常见问题

### Q: 如何知道配置是否生效？
A: 启动时会显示加载的配置文件路径和使用的API端点。

### Q: 可以同时使用多个不同的API服务吗？
A: 可以，通过分别配置 `EMBEDDING_*` 和 `GENERATOR_*` 变量。

### Q: 模型名称如何确定？
A: 请参考你使用的API服务的文档，通常可以在API文档中找到支持的模型列表。