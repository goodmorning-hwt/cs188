# README

## Notes

to edit: `search.py`, `searchAgent.py`
to look: `pacman.py`, `game.py`, `util.py`

## pacman.py

### 主要接口（Accessor Methods 和核心功能）
这些方法用于访问游戏状态数据或生成新的游戏状态。

1. **getAndResetExplored()**  
   - **静态方法**  
   - 描述：返回已探索状态的副本并重置`explored`集合。  
   - 返回：已探索状态的集合。

2. **getLegalActions(agentIndex=0)**  
   - 描述：返回指定代理（默认是Pacman，索引0）的合法动作列表。  
   - 参数：`agentIndex` - 代理索引（0表示Pacman，其他表示Ghost）。  
   - 返回：合法动作列表，若游戏结束（Win或Lose）则返回空列表。

3. **generateSuccessor(agentIndex, action)**  
   - 描述：根据指定代理的动作生成后续状态。  
   - 参数：
     - `agentIndex` - 代理索引。
     - `action` - 代理执行的动作。
   - 返回：新的`GameState`对象（后续状态）。  
   - 备注：处理Pacman或Ghost的动作效果、时间惩罚、死亡检查等。

4. **getLegalPacmanActions()**  
   - 描述：返回Pacman的合法动作列表（调用`getLegalActions(0)`）。  
   - 返回：Pacman的合法动作列表。

5. **generatePacmanSuccessor(action)**  
   - 描述：根据Pacman的动作生成后续状态（调用`generateSuccessor(0, action)`）。  
   - 参数：`action` - Pacman的动作。  
   - 返回：新的`GameState`对象。

6. **getPacmanState()**  
   - 描述：返回Pacman的代理状态（`AgentState`对象，包含位置和方向）。  
   - 返回：Pacman的`AgentState`副本。

7. **getPacmanPosition()**  
   - 描述：返回Pacman的当前位置。  
   - 返回：Pacman的坐标`(x, y)`。

8. **getGhostStates()**  
   - 描述：返回所有Ghost的代理状态列表。  
   - 返回：Ghost的`AgentState`对象列表（不包括Pacman）。

9. **getGhostState(agentIndex)**  
   - 描述：返回指定Ghost的代理状态。  
   - 参数：`agentIndex` - Ghost的索引（不能为0）。  
   - 返回：指定Ghost的`AgentState`对象。  
   - 异常：如果索引无效（0或超出范围），抛出异常。

10. **getGhostPosition(agentIndex)**  
    - 描述：返回指定Ghost的当前位置。  
    - 参数：`agentIndex` - Ghost的索引（不能为0）。  
    - 返回：指定Ghost的坐标`(x, y)`。  
    - 异常：如果索引为0，抛出异常。

11. **getGhostPositions()**  
    - 描述：返回所有Ghost的当前位置列表。  
    - 返回：包含所有Ghost坐标`(x, y)`的列表。

12. **getNumAgents()**  
    - 描述：返回游戏中代理的总数（Pacman + Ghosts）。  
    - 返回：代理数量（整数）。

13. **getScore()**  
    - 描述：返回当前游戏的分数。  
    - 返回：分数（浮点数）。

14. **getCapsules()**  
    - 描述：返回剩余胶囊的位置列表。  
    - 返回：胶囊坐标`(x, y)`的列表。

15. **getNumFood()**  
    - 描述：返回剩余食物的数量。  
    - 返回：食物数量（整数）。

16. **getFood()**  
    - 描述：返回表示食物分布的布尔网格（`Grid`对象）。  
    - 返回：`Grid`对象，可通过`food[x][y]`检查某位置是否有食物。

17. **getWalls()**  
    - 描述：返回表示墙壁分布的布尔网格（`Grid`对象）。  
    - 返回：`Grid`对象，可通过`walls[x][y]`检查某位置是否有墙壁。

18. **hasFood(x, y)**  
    - 描述：检查指定位置是否有食物。  
    - 参数：`x`, `y` - 坐标。  
    - 返回：布尔值（`True`表示有食物）。

19. **hasWall(x, y)**  
    - 描述：检查指定位置是否有墙壁。  
    - 参数：`x`, `y` - 坐标。  
    - 返回：布尔值（`True`表示有墙壁）。

20. **isLose()**  
    - 描述：检查游戏是否失败。  
    - 返回：布尔值（`True`表示失败）。

21. **isWin()**  
    - 描述：检查游戏是否胜利。  
    - 返回：布尔值（`True`表示胜利）。

---

### 辅助接口（Helper Methods）
这些方法通常不建议直接调用，主要用于内部实现。

1. **__init__(prevState=None)**  
   - 描述：初始化游戏状态，可从前一状态复制数据。  
   - 参数：`prevState` - 前一状态（可选，默认为`None`表示初始状态）。  
   - 备注：如果没有前一状态，创建新的`GameStateData`对象。

2. **deepCopy()**  
   - 描述：创建当前状态的深拷贝。  
   - 返回：新的`GameState`对象（深拷贝）。

3. **__eq__(other)**  
   - 描述：比较两个状态是否相等（基于`GameStateData`）。  
   - 参数：`other` - 另一个`GameState`对象。  
   - 返回：布尔值（`True`表示相等）。

4. **__hash__()**  
   - 描述：返回状态的哈希值，允许状态作为字典键。  
   - 返回：哈希值（基于`GameStateData`）。

5. **__str__()**  
   - 描述：返回状态的字符串表示。  
   - 返回：`GameStateData`的字符串形式。

6. **initialize(layout, numGhostAgents=1000)**  
   - 描述：根据布局初始化游戏状态。  
   - 参数：
     - `layout` - 游戏布局（来自`layout.py`）。
     - `numGhostAgents` - Ghost数量（默认为1000，实际受布局限制）。  
   - 备注：调用`GameStateData.initialize`设置初始状态。

## Game.py

### 1. **Agent 类**
- **构造函数**:
  - `__init__(self, index=0)`: 初始化代理，设置代理的索引。
- **主要接口**:
  - `getAction(self, state)`: **必须实现**，接收游戏状态 (`GameState`)，返回一个方向动作（`Directions.{North, South, East, West, Stop}`）。
- **可选接口**:
  - `registerInitialState(self, state)`: 可选方法，用于检查初始游戏状态。

---

### 2. **Directions 类**
- **静态变量**:
  - `NORTH`, `SOUTH`, `EAST`, `WEST`, `STOP`: 表示方向的常量字符串。
- **方向映射**:
  - `LEFT`: 字典，定义每个方向向左旋转的结果（例如，`NORTH` -> `WEST`）。
  - `RIGHT`: 字典，定义每个方向向右旋转的结果（由 `LEFT` 反向生成）。
  - `REVERSE`: 字典，定义每个方向的反向（例如，`NORTH` -> `SOUTH`）。

---

### 3. **Configuration 类**
- **构造函数**:
  - `__init__(self, pos, direction)`: 初始化配置，包含位置 `(x, y)` 和方向。
- **主要接口**:
  - `getPosition(self)`: 返回当前位置 `(x, y)`。
  - `getDirection(self)`: 返回当前方向。
  - `isInteger(self)`: 检查位置坐标是否为整数。
  - `generateSuccessor(self, vector)`: 根据动作向量生成新的配置（低级调用，不检查移动合法性）。
- **其他接口**:
  - `__eq__(self, other)`: 比较两个配置是否相等。
  - `__hash__(self)`: 生成配置的哈希值。
  - `__str__(self)`: 返回配置的字符串表示，例如 `(x,y)=(1,2), North`。

---

### 4. **AgentState 类**
- **构造函数**:
  - `__init__(self, startConfiguration, isPacman)`: 初始化代理状态，包含初始配置、是否为 Pacman、恐惧计时器等。
- **主要接口**:
  - `getPosition(self)`: 返回代理当前位置。
  - `getDirection(self)`: 返回代理当前方向。
  - `copy(self)`: 创建代理状态的副本。
- **其他接口**:
  - `__str__(self)`: 返回状态的字符串表示（例如，`"Pacman: (x,y)=(1,2), North"` 或 `"Ghost: ..."`）。
  - `__eq__(self, other)`: 比较两个代理状态是否相等。
  - `__hash__(self)`: 生成代理状态的哈希值。
- **属性**:
  - `start`: 初始配置。
  - `configuration`: 当前配置。
  - `isPacman`: 是否为 Pacman（布尔值）。
  - `scaredTimer`: 恐惧状态计时器。
  - `numCarrying`: 携带的物品数量。
  - `numReturned`: 返回的物品数量。

---

### 5. **Grid 类**
- **构造函数**:
  - `__init__(self, width, height, initialValue=False, bitRepresentation=None)`: 初始化二维网格，指定宽度、高度、初始值（布尔值）或位表示。
- **主要接口**:
  - `__getitem__(self, i)`: 获取网格第 `i` 列的数据（`grid[x]`）。
  - `__setitem__(self, key, item)`: 设置网格第 `key` 列的数据。
  - `copy(self)`: 创建网格的深拷贝。
  - `deepCopy(self)`: 同 `copy`，创建深拷贝。
  - `shallowCopy(self)`: 创建网格的浅拷贝。
  - `count(self, item=True)`: 统计网格中指定值（默认为 `True`）的数量。
  - `asList(self, key=True)`: 返回网格中值为 `key` 的位置列表 `[(x, y), ...]`。
  - `packBits(self)`: 将网格打包为位表示（返回元组 `(width, height, bitPackedInts...)`）。
- **内部接口**:
  - `_cellIndexToPosition(self, index)`: 将单元索引转换为 `(x, y)` 位置。
  - `_unpackBits(self, bits)`: 从位表示解包数据填充网格。
  - `_unpackInt(self, packed, size)`: 将整数解包为布尔值列表。
- **其他接口**:
  - `__str__(self)`: 返回网格的字符串表示（Pacman 地图风格，左下角为 `(0,0)`）。
  - `__eq__(self, other)`: 比较两个网格是否相等。
  - `__hash__(self)`: 生成网格的哈希值。

---

### 6. **全局函数**
- `reconstituteGrid(bitRep)`: 从位表示 `(width, height, bitPackedInts...)` 恢复网格对象。

---

### 总结
- **核心接口**:
  - `Agent.getAction`: 代理决策的核心方法。
  - `Configuration.getPosition`, `Configuration.getDirection`: 获取位置和方向。
  - `AgentState.getPosition`, `AgentState.getDirection`: 代理状态的位置和方向。
  - `Grid` 的数据访问（`__getitem__`, `__setitem__`）和拷贝（`copy`, `deepCopy`）。
- **辅助接口**:
  - 方向映射（`Directions.LEFT`, `RIGHT`, `REVERSE`）。
  - 网格的位打包/解包（`Grid.packBits`, `Grid._unpackBits`）。
  - 配置和状态的比较、哈希和字符串表示。


## util.py