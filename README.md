# CFRI 网络学院题库

国家消防救援网络学院（https://wy.cfri.edu.cn）课后考试题库，供「网院免维护版」油猴脚本云端调用。

- `cfri-bank.json`：题库文件，纯 JSON
- 文件名不要改（脚本默认按这个名字找）

## 格式

```json
{
  "<题干指纹>": {
    "a": [正确选项下标，从 0 开始],
    "n": 选项个数,
    "t": 题型（1 单选 / 2 多选 / 3 判断）,
    "q": "题干（仅供人看，脚本不用）"
  }
}
```

- 键是 `hash32(题型 + "|" + 规整后的题干)`，题干规整规则：去掉标签、空白、标点。
- 判断题 `a` 里：`[0]`=正确，`[1]`=错误。
- 多选题如 `[0,1,2]` 表示 A、B、C。

## 上传方式 A：网页上传（不需要 git）

1. GitHub 右上角 **New repository** → 名字如 `cfri-bank` → 选 **Public** → Create。
2. 仓库页 **Add file → Upload files**，把 `cfri-bank.json` 拖进去 → **Commit changes**。
3. 打开 `cfri-bank.json` → 右上 **Raw** → 复制地址，形如：
   `https://raw.githubusercontent.com/你的用户名/cfri-bank/main/cfri-bank.json`
4. 打开脚本面板 → **设置** → 「云端题库地址」粘贴 → **保存并同步云端题库**。
5. 想更快可以换成 jsDelivr 地址：
   `https://cdn.jsdelivr.net/gh/你的用户名/cfri-bank@main/cfri-bank.json`

## 上传方式 B：脚本一键上传（需要 Token）

1. GitHub → Settings → Developer settings → **Personal access tokens** → 生成
   - Classic：勾 `repo`（公开仓库勾 `public_repo` 即可）
   - Fine-grained：只授权目标仓库的 **Contents: Read and write**
2. 脚本面板 → 设置 → 填：
   - GitHub 用户名/组织：`你的用户名`
   - 仓库名：`cfri-bank`
   - 文件路径：`cfri-bank.json`
   - GitHub Token：刚生成的令牌
3. 点 **上传题库到 GitHub**，日志会显示「已上传 GitHub：N 题」。
4. Token 只存在本机 `localStorage`，不会发给除 api.github.com 以外的任何地方。

## 脚本怎么用这份题库

合并优先级：**本机收割（最可信） > 云端题库 > 脚本内置**。

- 启动时若配置了地址，会拉一次（本地缓存 6 小时）
- 点「更新题库」会强制重新拉取，并重扫本班所有已考完的考试
- 判断题在接口里只回 1 个选项副本，所以脚本对判断题不做「选项数一致」校验

## 注意

- 题库来自真实作答记录，**公开到 GitHub 等于公开答案**，仓库建议只放题库、别放账号姓名。
- 平台改版/换题后：脚本交卷会自动追加新题，重新上传一次即可。
- 私有仓库的 raw 地址需要带 Token，脚本暂不带，建议用 Public 仓库。
