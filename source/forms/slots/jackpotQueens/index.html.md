---
title: Slot No.88 JackpotQueens Message Protocols

language_tabs: # must be one of https://git.io/vQNgJ
  - json

toc_footers:
  - <a href='https://alansynn.com'>Documented by Alan Synn</a>
  - Rev 2.0

includes:
  - slot

search: false
print: false
---

# Slot No.88 JackpotQueens 메시지 프로토콜 소개 문서

### Rev 2.0
이하 호출 프로토콜에서 기본으로 필요한 `SIG_SLOT protocol`은 설명에서 제외.

## 수정내역
### Rev 1.0
2019-07-19 18:00 

+ 기본 스핀

### Rev 2.0
2019-07-30 16:00

+ 피쳐들 추가
+ 변경 플로우 반영

# 슬롯(룸) 입장

> Request

```javascript
// Signal Handler on Client side
handle_signal: function( msg ) {
    switch( msg.protocol ) {
        case SIG.SIG_SET_SLOT: {
            ...
        }
            break;
        ...
```

> Response  
> 상대적으로 긴 정보는 ... 으로 표시.

```json
{
    "code": 200,
    "gameID": 88,
    "rid": -1,
    "gameInfo": {
        "betTable": [250,500,1000,2500,5000,10000,25000,50000,100000,250000,500000,1000000,2500000,5000000,10000000,25000000,50000000,100000000,250000000,500000000,1000000000,2500000000,5000000000,10000000000],
        "betLimit": [ { "level": 2, "bet": 20000 }, { "level": 6, "bet": 40000 }, { "level": 9, "bet": 80000 } ],
        "betIndex": -1,
        "betLines": 30,
        "betPerLine": 0,
        "parSheet": {
            "TEST_MODE": false,
            "debugFunction":["toMajorWin"],
            "betTable": [250,500,1000,2500,5000,10000,25000,50000,100000,250000,500000,1000000,2500000,5000000,10000000,25000000,50000000,100000000,250000000,500000000,1000000000,2500000000,5000000000,10000000000],
            "payLines": ["0x11111","0x00000","0x22222","0x01210","0x21012","0x00100","0x22122","0x12221","0x10001","0x01110","0x21112","0x01010","0x21212","0x10101","0x12121","0x11011","0x11211","0x02020","0x20202","0x10201","0x12021","0x00200","0x22022","0x02220","0x20002","0x02120","0x20102","0x11222","0x22100","0x00011"],
            "symbols": [
                {"id":71,"name":"Empty","type":0,"typifyName":"jqSymScatter1AR"},
                ...
            ],
            "reels":[
                {
                    "index":0,
                    "strip":[71,91,71,22,71,11,71,21,71,12,71,23,71,91,71,12,71,11,71,21,71,23,71,22,71,91,71,21,71,22,71,11,71,12,71,23,71,91,71,12,71,12,71,21,71,11,71,11],
                    "weight0":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
                    "weight1":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
                    "weight2":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
                    "weight3":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
                    "weight4":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1]
                },
                ...
            ],
            "jackpotBonusScatterSymID":91,
            "BonusScatterSymID":92,
            "WildSymID":1,
            "MajorSymIDs":[11,12],
            "MinorSymIDs":[21,22,23],
            "EmptySymID":71,
            "customAction":{
                "bonusGame": 1,
                "jackpotBonusGame": 2,
                "freeSpinGame": 3,
                "claimFreeSpinWin": 4
            },
            "jackpotLimitBet":50000
        },
    "maxLine":30
    },
    "gameParams":null
}
```

### SET SLOT

#### Sequence Diagram
<div class="mermaid">
    sequenceDiagram
        participant C as Client
        participant S as Server
        participant D as DB
        C->>S: 게임 접속
        S->>D: Request user data
        Note right of D: ex: userInfo, slotBuff
        activate D
        D-->>S: user data
        deactivate D
        S->>C: 게임 접속 데이터
        C->>S: 슬롯 입장
        S->>D: Request user slot sync data
        activate D
        D-->>S: Slot Sync Data
        deactivate D
        alt 동기화 데이터가 존재할 때
            S-->>C: json(gameInfo + syncParams)
        else 동기화 데이터가 없을때
            S-->>C: json(gameInfo)
        end
</div>

# In game

## Spin

> Request  

```javascript
// Signal Handler on Client side
handle_signal: function( msg ) {
    switch( msg.protocol ) {
        case SIG.SIG_SPIN_SLOT: {
            ...
        }
            break;
        ...
```

> Response Type 1

```json
{
    "protocol":100,
    "code":200,
    "rands":[37,0,4,39,23],
    "result":[
        {"win":2,"matchSymbolID":[21,22,23],"name":"mixed","matchCount":3,"lineIndex":7,"matchPos":[0,1,2]},
        {"win":2,"matchSymbolID":[21,22,23],"name":"mixed","matchCount":3,"lineIndex":19,"matchPos":[0,1,2]}
    ],
    "totalWin":0,
    "winInfo":{
        "isMajorWin":false,
        "majorWinIndex":-1,
        "multiple":0,
        "lineMultiple":0
    },
    "isBonusGame":true,
    "isJackpotBonusGame":false
}
```

> Response Type 2

```json
{
    "protocol":100,
    "code":200,
    "rands":[37,0,4,39,23],
    "result":[
        {"win":2,"matchSymbolID":[21,22,23],"name":"mixed","matchCount":3,"lineIndex":7,"matchPos":[0,1,2]},
        {"win":2,"matchSymbolID":[21,22,23],"name":"mixed","matchCount":3,"lineIndex":19,"matchPos":[0,1,2]}
    ],
    "totalWin":0,
    "winInfo":{
        "isMajorWin":false,
        "majorWinIndex":-1,
        "multiple":0,
        "lineMultiple":0
    },
    "isBonusGame":false,
    "isJackpotBonusGame":true
}
```

> Response Type 3

```json
{
    "protocol":100,
    "code":200,
    "rands":[37,0,4,39,23],
    "result":[
        {"win":2,"matchSymbolID":[21,22,23],"name":"mixed","matchCount":3,"lineIndex":7,"matchPos":[0,1,2]},
        {"win":2,"matchSymbolID":[21,22,23],"name":"mixed","matchCount":3,"lineIndex":19,"matchPos":[0,1,2]}
    ],
    "totalWin":0,
    "winInfo":{
        "isMajorWin":false,
        "majorWinIndex":-1,
        "multiple":0,
        "lineMultiple":0
    },
    "isBonusGame":false,
    "isJackpotBonusGame":false
}
```

> Error Response

```json
{
    "protocol":100,
    "code":4006
}
```

### Sequence Diagram
<div class="mermaid">
    sequenceDiagram
        participant C as Client
        participant S as Server
        participant D as DB
        C->>S: Spin Request
        alt isBonusGame === true
            S->>+D: Request jackpot pool(progressive amount)
            D-->>-S: Get jackpot pool info
            S --> S: Store currJackpotInfo
            S-->>C: json(Response Type1)
        else isJackpotBonusGame === true
            S->>+D: Request jackpot pool(progressive amount)
            D-->>-S: Get jackpot pool info
            S --> S: Store currJackpotInfo
            S-->>C: json(Response Type2)
        end
        opt 당첨없음
            S-->>C: json(Response Type3)
        end
</div>

### Response Parameters

Rev | Parameter | Default | Description
--------- | --------- | ------- | -----------
1|protocol | int(100) | SIG_SLOT_SPIN
1|code | int(200) | 서버 OK 리스폰스 넘버
1|rands | int(0-스트립길이) Array(5) | 랜드값
1|result | object Array | 획득 결과 내용
1|totalWin | int(0-max) | 획득 결과 금액
1|isBonusGame | boolean | 보너스게임 당첨 여부
1|isJackpotBonusGame | boolean | 잭팟보너스게임 당첨 여부
1|winInfo | object | 획득 정보에 대한 판정을 담은 객체
1|winInfo.isMajorWin | boolean | 메이져 윈 여부
1|winInfo.majorWinIndex | int(-1-4) | 메이져윈일 경우의 인덱스
1|winInfo.multiple | int(0-max) | 당첨금액/총배팅액 결과
1|winInfo.lineMultiple | int(0-max) | 당첨금액/라인배팅액 결과

### Response Parameters in DEBUG

Parameter | Default | Description
--------- | ------- | -----------
DEBUG_GRID | int Array(3x5) | 디버그용 랜드심볼아이디(row순) 

## Jackpot Bonus Game

> Request  

```javascript
// Define Signal From parSheet
var SIG.JACKPOT_BONUS_GAME = this.parSheet.actions.jackpotBonusGame;

// Signal Handler on Client side
RockN.NET.request( 'connector.gameHandler.request', {
        protocol: SIG.SIG_SLOT_CUSTOM_ACTION,
        action: SIG.JACKPOT_BONUS_GAME,
        playerID: RockN.Player.playerID,
    }, func..
```

> Response

```json
{
    "protocol":120,
    "action":2,
    "code":200,
    "win":600,
    "rand":1,
    "randId":42,
    "jackpotType":"JackpotMajor",
    "jackpotIndex":2,
    "currJackpotInfo":[90,240,600,3000,30000],
    "isFreeSpinMode":false
}
```

> Error Response

```json
{
    "protocol":120,
    "action":2,
    "code":500
}
```

### Sequence Diagram
<div class="mermaid">
    sequenceDiagram
        participant C as Client
        participant S as Server
        participant D as DB
        C ->>S: Jackpot Bonus Game Request
        S ->>+D: Initiate Jackpot Info on jackpotIndex
        D -->>-S: Get Initiated JackpotInfo on jackpotIndex
        S ->>S: Change to non-progressive jackpotInfo on jackpotIndex
        S -->>C: json(Response)
</div>

### Response Parameters

Rev | Parameter | Default | Description
--------- | --------- | ------- | -----------
1|protocol | int(120) | SIG_SLOT_CUSTOM_ACTION
1|action | int(2) | customAction 인덱스
1|code | int(200) | 서버 OK 리스폰스 넘버
1|rand | int(0-스트립길이) | 랜드값
1|randId | int(symbolId) | 랜드한 심볼 아이디
1|jackpotType | string | 잭팟 타입
1|jackpotIndex | int(0-4) | 잭팟 인덱스
1|currJackpotInfo | int(기본 잭팟값-max) Array(5) | 갱신한 잭팟 정보
1|isFreeSpinMode | boolean | 현재 프리스핀 모드인지 여부

## Bonus Game
`Rev2.0 변경사항` : 현 Bonus Game은 기획서의 EachWin Wheel을 의미, 보너스게임 진행 후 프리스핀 진행  

> Request  

```javascript
// Define Signal From parSheet
var SIG.BONUS_GAME = this.parSheet.actions.bonusGame;

// Signal Handler on Client side
RockN.NET.request( 'connector.gameHandler.request', {
        protocol: SIG.SIG_SLOT_CUSTOM_ACTION,
        action: SIG.BONUS_GAME,
        playerID: RockN.Player.playerID,
    }, func..
```

> Response

```json
{
    "protocol":120,
    "action":1,
    "code":200,
    "eachWin":165,
    "rand":5,
    "randIds":[54],
    "initFreeSpinCount":3
}
```

> Error Response

```json
{
    "protocol":120,
    "action":1,
    "code":500
}
```

### Sequence Diagram
<div class="mermaid">
    sequenceDiagram
        participant C as Client
        participant S as Server
        C ->>S: Bonus Game Request
        S -->>C: json(Response)
</div>

### Response Parameters

Rev | Parameter | Default | Description
--------- | --------- | ------- | -----------
1|protocol | int(120) | SIG_SLOT_CUSTOM_ACTION
1|action | int(1) | customAction 인덱스
1|code | int(200) | 서버 OK 리스폰스 넘버
1|eachWin | int(0-max) | 획득한 EachWin 값
1|rand | int(0-스트립길이) | 랜드값
1|randIds | int(symId) Array(1) | 랜드한 심볼 아이디
1|initFreeSpinCount | int(3) | 시작한(현재 남은) 프리스핀 카운트

## FreeSpin

> Request  

```javascript
// Define Signal From parSheet
var SIG.FREESPIN_GAME = this.parSheet.actions.freeSpinGame;

// Signal Handler on Client side
RockN.NET.request( 'connector.gameHandler.request', {
        protocol: SIG.SIG_SLOT_CUSTOM_ACTION,
        action: SIG.FREESPIN_GAME,
        playerID: RockN.Player.playerID,
    }, func..
```

> Response

```json
{
    "protocol":120,
    "action": 3,
    "code":200,
    "rands":[29,44,29,19,36],
    "result":[
        {"win":2,"matchSymbolID":[21,22,23],"name":"mixed","matchCount":3,"lineIndex":13}
    ],
    "eachWinResult":[
        {"x":3,"y":1,"win":30,"name":"eachWin"}
    ],
    "currWin":32,
    "freeSpinTotalWin":62,
    "freeSpinCount":2,
    "is2ndChance":true,
    "isRefreshSpinCount":true,
    "isJackpotBonusGame":true
}
```

> Error Response

```json
{
    "protocol":120,
    "action":3,
    "code":500
}
```


### Sequence Diagram
<div class="mermaid">
    sequenceDiagram
        participant C as Client
        participant S as Server
        C ->>S: FreeSpin Game Request
        S -->>C: json(Response)
</div>

### Response Parameters

Rev | Parameter | Default | Description
--------- | --------- | ------- | -----------
1|protocol | int(120) | SIG_SLOT_CUSTOM_ACTION
1|action | int(3) | customAction 인덱스
1|code | int(200) | 서버 OK 리스폰스 넘버
1|rands | int(0-스트립길이) Array(5) | 랜드값
1|result | object Array | 획득 결과 내용
1|eachWinResult | object Array | eachWin 획득 결과 오브젝트
1|eachWinResult.x | int(0-4) | eachWin 획득 심볼 x축 좌표
1|eachWinResult.y | int(0-2) | eachWin 획득 심볼 y축 좌표
1|eachWinResult.win | int(0-max) | eachWin 획득 심볼 win 금액
1|eachWinResult.name | string | (ex. "eachWin")
1|currWin | int(0-max) | 이번 스핀 획득금액
1|freeSpinTotalWin | int(0-max) | 프리스핀 총 획득금액
1|is2ndChance | boolean | is2ndChance 팝업
1|isRefreshSpinCount | boolean | 스핀 추가 여부
1|isJackpotBonusGame | boolean | 잭팟 보너스 게임 진입 여부

## Claim FreeSpin Win

> Request  

```javascript
// Define Signal From parSheet
var SIG.CLAIM_FREESPIN_WIN = this.parSheet.actions.claimFreeSpinWin;

// Signal Handler on Client side
RockN.NET.request( 'connector.gameHandler.request', {
        protocol: SIG.SIG_SLOT_CUSTOM_ACTION,
        action: SIG.CLAIM_FREESPIN_WIN,
        playerID: RockN.Player.playerID,
    }, func..
```

> Response

```json
{
    "protocol":120,
    "action":4,
    "code":200,
    "totalWin": 23450,
    "initFreeSpinCount": 9
}
```

> Error Response

```json
{
    "protocol":120,
    "action":4,
    "code":500
}
```

### Sequence Diagram
<div class="mermaid">
    sequenceDiagram
        participant C as Client
        participant S as Server
        C ->>S: Bonus Game Request
        S -->>C: json(Response)
</div>

### Response Parameters

Rev | Parameter | Default | Description
--------- | --------- | ------- | -----------
1|protocol | int(120) | SIG_SLOT_CUSTOM_ACTION
1|action | int(4) | customAction 인덱스
1|code | int(200) | 서버 OK 리스폰스 넘버
1|totalWin | int(0-max) | 피쳐 중 획득한 총 금액 값
1|initFreeSpinCount | int(3-max) | 피쳐 중 돌았던 총 프리스핀 카운트

## Get Jackpot Info

> Request  

```javascript
// Signal Handler on Client side
RockN.NET.request( 'connector.gameHandler.request', {
        protocol: SIG.SIG_GET_SLOT_JACKPOT_INFO,
        playerID: RockN.Player.playerID,
        totalBet: totalBet / this._owner.slotMenu.getBetLines() * this._owner.DEFINES.PAY_LINES
    }, func..
```

> Response

```json
{
    "protocol":112,
    "code":200,
    "betCash":10,
    "info":[30,80,200,1000,10000]
}
```

> Error Response

```json
{
    "protocol":112,
    "code":500
}
```

### Sequence Diagram
<div class="mermaid">
    sequenceDiagram
        participant C as Client
        participant S as Server
        participant D as DB
        C ->>S: Jackpot Bonus Game Request
        alt NormalMode
            S ->>+D: Get progressive jackpotInfo
            D -->>-S: Response
        else currMode != NormalMode
            S -->S: Get JackpotInfo from currJackpotInfo
        end
        S ->>C: json
</div>

### Response Parameters

Rev | Parameter | Default | Description
--------- | --------- | ------- | -----------
1|protocol | int(112) | SIG_GET_SLOT_JACKPOT_INFO
1|code | int(200) | 서버 OK 리스폰스 넘버
1|betCash | int | 유저가 배팅한 금액
1|info | int Array(5) | jackpotInfo - 노멀모드일 경우에는 실시간 갱신이나 노멀이 아닐 경우 서버에 저장된 currJackpotInfo(피쳐 진입시 저장)를 받음

# Sync
## FlowChart
<div class="mermaid">
graph TD
    S[신규진입 초기화 상태 == no SyncParams] -->F1(Spin Request)
    F1 --> R[onSpinResponse 수신 및 클라이언트 동작 완료 : 동기화 포인트1]
    R --> B{onSpinResponse}
    B -->|isJackpotBonusGame == true| F3>jackpotBonusGame 진입 및 팝업]
    F3 --> F3-1(jackpotBonusGame Request)
    F3-1 --> F3-2[jackpotBonusGameResponse 수신 및 클라이언트 동작 완료 : 동기화 포인트2]
    F3-2 --> Q(ClaimJackpotBonusGameWin 추가??)
    Q --> F2
    B -->|isBonusGame == true| F2>BonusGame 진입 및 팝업]
    F2 --> F2-1(BonusGame Request)
    F2-1 --> F2-2[BonusGameResponse 수신 및 클라이언트 동작 완료 : 동기화 포인트3]
    F2-2 --> Q2(ClaimBonusGameWin 추가??)
    Q2 --> F4>프리스핀 진입 및 팝업]
    F4 --> F4-R(프리스핀 Request)
    F4-R --> F4-1[프리스핀Response 수신 : 동기화 포인트4]
    F4-1 --> F4-Q{onFreeSpinResponse}
    F5-3 --> F4-R
    F4-Q --> |is2ndChance == true?| F4-2>프리스핀 2nd Chance 팝업]
    F4-Q --> |else| F4-3
    F4-Q --> |isJackpotBonus == true?| F5-1>프리스핀 중 JackpotBonusGame 진입 및 팝업]
    subgraph JackpotBonusGameInFreeSpin
    F5-1 --> F5-2[JackpotBonusGame]
    F5-2 --> F5-3[JackpotBonusGame]
    end
    F4-2 --> F4-3[프리스핀 클라이언트 동작 완료]
    F4-3 --> F4-R
    F4-3 --> F4-Q2(claimFreeSpinWin)
    F4-Q2 --> F4-4>프리스핀 종료 팝업]
    F4-4 --> E[피쳐 종료]
    style R fill:#ED5752
    style F2-2 fill:#ED5752
    style F3-2 fill:#ED5752
    style F4-1 fill:#ED5752
    style Q fill:#808080
    style Q2 fill:#808080
    click R "#sync-point-1" "동기화 포인트1"
    click F2-2 "#sync-point-3" "동기화 포인트3"
    click F3-2 "#sync-point-2" "동기화 포인트2"
    click F4-1 "#sync-point-4" "동기화 포인트4"
</div>

## Sync Point 1

Rev | Parameter | Default | Description
--------- | --------- | ------- | -----------
1|isJackpotBonusGame | boolean | 
1|isBonusGame | boolean | 

## Sync Point 2

Rev | Parameter | Default | Description
--------- | --------- | ------- | -----------
1|isJackpotBonusGame | boolean | 
1|isBonusGame | boolean | 
1|jackpotWin | int(0-max) | jackpot금액

## Sync Point 3

Rev | Parameter | Default | Description
--------- | --------- | ------- | -----------
1|isJackpotBonusGame | boolean | 
1|isBonusGame | boolean | 
1|jackpotWin | int(0-max) | jackpot금액
1|eachWin | int(0-max) | eachWin금액

## Sync Point 4

Rev | Parameter | Default | Description
--------- | --------- | ------- | -----------
1|isJackpotBonusGame | boolean | 
1|isBonusGame | boolean | 
1|isFreeSpinMode | boolean | 
1|is2ndChancePopUp | boolean |
1|jackpotWin | int(0-max) | jackpot금액
1|eachWin | int(0-max) | eachWin금액
1|totalWin | int(0-max) | totalWin금액
1|freeSpinCount | int(0-max) | 남은 프리스핀 횟수
1|initFreeSpinCount | int(0-max) | 최초 진입시 프리스핀 횟수

# Protocols

<aside class="notice">
프로토콜 문서
</aside>

Slot No.88 JackpotQueens

Code | Meaning | Argument
---------- | ------- | -------
1 | bonusGame | None
2 | jackpotBonusGame | None
3 | claimFreeSpinWin | None