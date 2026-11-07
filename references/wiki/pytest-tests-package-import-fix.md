---
description: 当测试文件存在`from tests.xxx import ...`交叉引用且pytest报ModuleNotFoundError时，补加`tests/__init__.py`将目录声明为包是零功能改动的解决方案；需注意这可能改变测试收集语义，若原注释警告过则需权衡。
name: 测试环境pytest包导入修复
---

# 测试环境pytest包导入修复

当测试文件存在 `from tests.xxx import ...` 交叉引用且 pytest 报 `ModuleNotFoundError: No module named 'tests'` 时，在 `tests/` 目录补加 `__init__.py` 将测试目录声明为包，是零功能改动的修复方案。

## 原则

- **零功能改动**：只引入 `__init__.py`，不修改任何测试逻辑或生产代码，修复仅改变 Python 包识别方式而非行为。
- **改变收集语义**：该操作会改变 pytest 对测试目录的收集语义，若项目原注释警告过此风险（如影响插件或自定义收集规则），需先评估副作用再决定是否采用。
- **环境差异是根因**：同一份测试代码在不同环境或 pytest 版本下可能表现不同——上一轮全绿、本轮报错，往往是 `sys.path` / pytest 配置 / 收集顺序差异，而非代码缺陷。

## 区分

与真正的接线类缺陷不同，包导入失败表现为「已有测试全绿但新增文件无法运行」，属于环境/配置层缺口而非产品逻辑缺陷，可通过 接线类缺陷观察 的思路快速定位。

## 权衡

若原项目明确反对将 `tests/` 变为包，可改用 `pythonpath` 配置或调整 import 语句为相对导入；二者都会增加代码变动量，比补 `__init__.py` 的零功能改动更重。

## 例子

2026-10-06 实测中，`tests/test_reasoning_switch.py` 与 `tests/test_cancel_cooperative.py` 因 `from tests.test_seams_round1 import ...` 报 `ModuleNotFoundError`，补加 `tests/__init__.py` 后 7 个失败消失，2175 个测试全绿。

## Sources

- 该修复方案及其环境差异分析由 2026-10-06 会话记录 支持，其中记录了 7 个 ModuleNotFoundError 失败的根因与补 `__init__.py` 的验证结果。
- 与零功能改动原则及可见性纪律的一致性，可参考 自动修复要「动得可见」。
- 此类环境差异根因与接线类缺陷的观察方式，关联 把不变量写成会红的断言 中关于「结构上已满足不等于生效」的警示。
