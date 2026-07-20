# UML 图设计

## 用例图

```mermaid
flowchart TD
    User((用户))
    
    User -->|注册/登录| UC1[用户管理]
    User -->|情绪自评| UC2[情绪评估]
    User -->|选择训练| UC3[呼吸训练]
    User -->|选择训练| UC4[正念冥想]
    User -->|选择训练| UC5[自然场景]
    User -->|选择训练| UC6[音乐放松]
    User -->|选择训练| UC7[交互游戏]
    User -->|查看记录| UC8[历史数据]
    User -->|系统设置| UC9[系统设置]
```

## 类图（核心类）

```
┌─────────────────────┐
│    GameManager      │
├─────────────────────┤
│ - instance: static  │
│ - userData: UserData│
│ - currentState     │
├─────────────────────┤
│ + Awake()          │
│ + Start()          │
│ + LoadScene()      │
│ + SaveData()       │
│ + LoadData()       │
└─────────┬───────────┘
          │
┌─────────┴──────────────┐
│     UserData           │
├────────────────────────┤
│ - userId: int         │
│ - userName: string    │
│ - records: List<Record>│
├────────────────────────┤
│ + AddRecord()         │
│ + GetHistory()        │
│ + GetStatistics()     │
└────────────────────────┘

┌──────────────────────┐     ┌──────────────────────┐
│   EmotionAssessment  │     │   EmotionRecord      │
├──────────────────────┤     ├──────────────────────┤
│ - preScore: int     │     │ - recordId: int      │
│ - postScore: int    │     │ - dateTime: DateTime │
│ - anxietyLevel: int │     │ - preScore: int      │
├──────────────────────┤     │ - postScore: int     │
│ + StartAssessment() │     │ - trainingType: enum │
│ + SubmitScore()     │     │ - duration: float    │
│ + ShowResult()      │     ├──────────────────────┤
└──────────────────────┘     │ + ToJSON()           │
                             │ + FromJSON()         │
                             └──────────────────────┘

┌──────────────────────┐
│   BreathingGuide     │
├──────────────────────┤
│ - phase: enum        │
│ - duration: float    │
│ - isActive: bool     │
├──────────────────────┤
│ + StartBreathing()   │
│ + UpdatePhase()      │
│ + StopBreathing()    │
│ + OnPhaseChanged()   │
└──────────────────────┘
```

## 时序图（训练流程示例）

```mermaid
sequenceDiagram
    participant User as 用户
    participant UI as UI界面
    participant GM as GameManager
    participant Trainer as 训练模块
    participant DB as SQLite
    
    User->>UI: 选择训练模块
    UI->>GM: 请求开始训练
    GM->>Trainer: 初始化训练场景
    Trainer->>UI: 显示训练引导
    User->>Trainer: 跟随引导训练
    Trainer->>UI: 实时反馈显示
    Note over User,Trainer: 训练进行中...
    User->>Trainer: 完成训练
    Trainer->>GM: 训练结束，返回结果
    GM->>DB: 保存训练记录
    DB-->>GM: 确认保存
    GM->>UI: 显示训练完成
    UI->>User: 展示反馈效果
```
