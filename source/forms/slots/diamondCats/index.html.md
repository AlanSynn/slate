---
title: Slot No.82 DiamondCats Message Protocols

language_tabs: # must be one of https://git.io/vQNgJ
  - json

toc_footers:
  - <a href='https://alansynn.com'>Documented by Alan Synn</a>
  - Rev 1.1

includes:
  - slot

search: true
print: true
---

# Slot No.82 DiamondCats 메시지 프로토콜 소개 문서
작성자 : 신동주 전임

### Rev 1.1
이하 호출 프로토콜에서 기본으로 필요한 `SIG_SLOT protocol`은 설명에서 제외.

## 수정내역
### Rev 1
2019-06-19 13:00 

+ 기본스핀, 휠게임

### Rev 1.1
2019-06-19 13:00 

+ 휠게임 결과에 `nextStrip` 추가
+ 스핀피쳐(`freeSpin`, `diamondSpin`, `superDiamondSpin`) 추가
+ 잭팟 안내(`Response on Jackpot`) 추가

# 슬롯(룸) 입장

## SET SLOT

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
> 상세사항은 Argument 탭 참조.

```json
{
    "code": 200,
    "gameID": 82,
    "rid": 0,
    "gameInfo": {
        "betTable": [ 2, 5, 10, 25, 50, 75, 60000 ],
        "betLimit": [ { "level": 2, "bet": 20000 }, { "level": 6, "bet": 40000 }, { "level": 9, "bet": 80000 } ],
        "betIndex": -1,
        "betLines": 50,
        "betPerLine": 10,
        "parSheet": {
            "TEST_MODE": false,
            "payLines": ["0x00000","0x11111","0x22222","0x33333","0x00100","0x33233","0x01010","0x32323","0x01110","0x32223","0x01210","0x32123","0x10001","0x23332","0x10101","0x23232","0x11011","0x22322","0x11211","0x22122","0x12121","0x21212","0x12221","0x21112","0x12321","0x21012","0x00123","0x33210","0x01001","0x32332","0x01123","0x32210","0x01232","0x32101","0x10012","0x23321","0x10123","0x23210","0x11012","0x22321","0x11233","0x22100","0x12100","0x21233","0x12210","0x21123","0x12333","0x21000","0x01233","0x32100"],
            "betTable": [2,5,10,25,50,75,60000],
            "symbols": [
                {"id":90,"type":0,"extraNum":10,"typifyName":"dcSymScatter_WheelAR"},
                {"id":1,"type":0,"extraNum":10,"typifyName":"dcSymWildAR"},
                {"id":11,"type":0,"extraNum":10,"typifyName":"dcSymMajor01_RedAR"},
                {"id":12,"type":0,"extraNum":10,"typifyName":"dcSymMajor02_PurpleAR"},
                {"id":13,"type":0,"extraNum":10,"typifyName":"dcSymMajor03_BlueAR"},
                {"id":14,"type":0,"extraNum":10,"typifyName":"dcSymMajor04_GreenAR"},
                {"id":15,"type":0,"extraNum":10,"typifyName":"dcSymMajor05_RingAR"},
                {"id":16,"type":0,"extraNum":10,"typifyName":"dcSymMajor06_CushionAR"},
                {"id":21,"type":0,"extraNum":10,"typifyName":"dcSymMinor01_SpadeAR"},
                {"id":22,"type":0,"extraNum":10,"typifyName":"dcSymMinor02_HeartAR"},
                {"id":23,"type":0,"extraNum":10,"typifyName":"dcSymMinor03_CloverAR"},
                {"id":24,"type":0,"extraNum":10,"typifyName":"dcSymMinor04_DiamondAR"}
            ],
            "wildReelWheel": {
                "strip":["W1","W13","W123","W15","W24","W25","W45","W2345"]
            },
            "reelArrayWheel": {
                "strip":["R2","R3","R2","R3","R2","R4","R3","R4"]
            },
            "freeSpinWheel": {
                "strip":[11,9,11,9,11,9,2,9]
            },
            "superWheel": {
                "strip":["EF1","EF2","EF3","EF4","EF5","EF6","EF7","EF8"]
            },
            "superPotBetLimit":50000,
            "jackpot": {
                "totalBetLimit":[50000]
            },
            "actions": {
                "catWheelGame": 0,
                "diamondWheelGame": 1,
                "superDiamondWheelGame": 2,
                "freeSpinGame": 3,
                "diamondSpinGame": 4,
                "superDiamondSpinGame": 5
            },
            "nextStrip": [
                [13,13,13,13,13,13,13,13,13,13,13,13,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
                [13,13,13,13,13,13,13,13,13,13,13,13,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
                [13,13,13,13,13,13,13,13,13,13,13,13,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
                [13,13,13,13,13,13,13,13,13,13,13,13,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
                [13,13,13,13,13,13,13,13,13,13,13,13,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14]
            ]
        },
        "maxLine": 50
    },
    "gameName": "diamondCats",
    "gameParams": null
} 
```

> Error Response

```json
```

# In game

## Spin

### Response Parameters

Parameter | Default | Description
--------- | ------- | -----------
protocol | int(100) | SIG_SLOT_SPIN
code | int(200) | 서버 OK 리스폰스 넘버
rands | int(0-스트립길이) Array(5) | 랜드값
result | object Array | 획득 결과 내용(잭팟일때는 `Response on Jackpot` 참조)
totalWin | int(0-max) | 획득한 총 금액(result의 합산)
isCatWheel | boolean | 캣휠피쳐(스캐터 3개)에 당첨되었는지 여부
nextStrip | int Array(스트립길이x5) | 다음번 스핀시 돌릴 스트립들
totalPotCount | int(0-200) | 현재까지 팟이 차오른 크기(팟이 터질시 0으로 초기화)
potStep | int(0-5) | 팟스텝, 몇번째 팟인지 여부(마지막 즉, 5번째라도 배팅금액이 일정금액 미만일시 isSuperPot이 아닌 isPot이 true가 되어 다이아몬드팟 피쳐로 진입)
isPot | boolean | 다이아몬드 팟 피쳐에 당첨되었는지 여부
isSuperPot | boolean | 슈퍼 다이아몬드 팟 피쳐에 당첨되었는지 여부

### Response Parameters in DEBUG

Parameter | Default | Description
--------- | ------- | -----------
DEBUG_FOR_CLIENT_GRID | int Array(5x4) | 랜드한 그리드 결과

> Request  
Spin 요청

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

> Response

```json
 {
    "protocol": 100,
    "code": 200,
    "rands":[36,17,10,49,0],
    "result":[
        {"win":120000,"matchSymbolID":16,"name":"CushionMajor","matchCount":3,"lineIndex":24,"wildCount":2},
        {"win":120000,"matchSymbolID":16,"name":"CushionMajor","matchCount":3,"lineIndex":46,"wildCount":2}
    ],
    "totalWin":240000,
    "isCatWheel":false,
    "DEBUG_FOR_CLIENT_GRID":[
        [90,14,21,1,14],[1,15,21,11,21],[11,16,21,12,21],[12,21,1,13,21]
    ],
    "nextStrip":[
        [24,24,24,90,90,90,90,90,24,24,24,24,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
        [24,24,24,90,90,90,90,90,24,24,24,24,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
        [24,24,24,90,90,90,90,90,24,24,24,24,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
        [24,24,24,90,90,90,90,90,24,24,24,24,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
        [24,24,24,90,90,90,90,90,24,24,24,24,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14]
    ],
    "totalPotCount":6,
    "potStep":1,
    "isPot":false,
    "isSuperPot":false
}
```

> Response on Jackpot

```json
 {
    "protocol": 100,
    "code": 200,
    "rands":[20,17,11,49,0],
    "result":[
        {"win":80000,"name":"Jackpot","matchSymbolID":1,"matchCount":50,"wildCount":50}
    ],
    "totalWin":240000,
    "isCatWheel":false,
    "DEBUG_FOR_CLIENT_GRID":[
        [1,1,1,1,1],[1,1,1,1,1],[1,1,1,1,1],[1,1,1,1,1]
    ],
    "nextStrip":[
        [24,24,24,90,90,90,90,90,24,24,24,24,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
        [24,24,24,90,90,90,90,90,24,24,24,24,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
        [24,24,24,90,90,90,90,90,24,24,24,24,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
        [24,24,24,90,90,90,90,90,24,24,24,24,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
        [24,24,24,90,90,90,90,90,24,24,24,24,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14]
    ],
    "totalPotCount":6,
    "potStep":1,
    "isPot":false,
    "isSuperPot":false
}
```

> Error Response

```json
```

## Cat Wheel Game

총 `2`번의 Request를 서버로 보냄.
1. 릴어레이 갯수 요청
2. 와일드릴의 갯수 요청 -> 모든 결과를 보냄

> Request (1-2번 모두 동일)    

```javascript
// Define Signal From parSheet
var SIG.CAT_WHEEL_GAME_SIGNAL = this.parSheet.actions.catWheelGame;

// Signal Handler on Client side
handle_signal: function( msg ) {
        switch( msg.protocol ) {
            case SIG.CAT_WHEEL_GAME_SIGNAL: {
                ...
            }
                break;
            ...
```

### 공통 Response Parameters

Parameter | Default | Description
--------- | ------- | -----------
protocol | int(120) | SIG_SLOT_CUSTOM_ACTION
action | int(0) | 파시트에서 받아온 상수
code | int(200) | 서버 OK 리스폰스 넘버
nextStep | int(-1 or 1) | 남은 휠게임 스텝의 리퀘스트 인덱스 넘버(-1이면 휠게임의 종료)

### 1번 Response Parameters

Parameter | Default | Description
--------- | ------- | -----------
rand | int(0-7) | 캣휠 릴 어레이 스트립의 랜드값
result | string | 캣휠 릴 어레이 스트립의 결과값

> 1번 Response

```json
{
    "protocol": 120,
    "action": 0,
    "code": 200,
    "nextStep":1,
    "rand":2,
    "result":"R2"
}
```

> Error Response

```json
```

### 2번 Response Parameters

Parameter | Default | Description
--------- | ------- | -----------
result | object | 캣휠 게임의 결과값이 들어있는 오브젝트
wheelStep1 | string | 캣휠 릴 어레이 스트립의 랜드값
wheelStep2 | string | 캣휠 와일드 릴 스트립의 랜드값
clientSetting | object | 클라이언트 세팅을 위한 파싱 결과가 담긴 오브젝트
reelArray | int(1-4) | (클라이언트에서) 세팅해야할 캣휠 릴 어레이 갯수
wildReels | int Array(0-5) | (클라이언트에서) 세팅해야할 와일드 스트립(와일드로 가득찬) 인덱스( 0이면 첫번째, 4이면 5번째 릴 )
remainSpinCount | int(1-max) | (클라이언트에서) 세팅해야할 프리스핀 횟수
nextStrip | int Array(스트립길이x5) | 다음번 프리스핀시 돌릴 스트립들

> 2번 Response

```json
{
    "protocol": 120,
    "action": 0,
    "code": 200,
    "nextStep":-1,
    "rand":3,
    "result": {
        "wheelStep1":"R2",
        "wheelShep2":"W15",
        "clientSetting": {
            "reelArray":2,
            "wildReels":[0,4]
        },
        "remainSpinCount":5,
        "nextStrip":[
            [11,11,11,11,11,11,11,11,11,11,11,11,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
            [11,11,11,11,11,11,11,11,11,11,11,11,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
            [11,11,11,11,11,11,11,11,11,11,11,11,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
            [11,11,11,11,11,11,11,11,11,11,11,11,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
            [11,11,11,11,11,11,11,11,11,11,11,11,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14]
        ]
    }
}
```

> Error Response

```json
```

## Diamond Wheel Game

총 `3`번의 Request를 서버로 보냄.
1. 프리스핀 횟수 요청
2. 릴어레이 갯수 요청
3. 와일드릴의 갯수 요청 -> 모든 결과를 보냄

### 공통 Response Parameters

Parameter | Default | Description
--------- | ------- | -----------
protocol | int(120) | SIG_SLOT_CUSTOM_ACTION
action | int(1) | 파시트에서 받아온 상수
code | int(200) | 서버 OK 리스폰스 넘버
nextStep | int(-1 or 1-2) | 남은 휠게임 스텝의 리퀘스트 인덱스 넘버(-1이면 휠게임의 종료)

> Request (1-3번 모두 동일)    

```javascript
// Define Signal From parSheet
var SIG.DIAMOND_WHEEL_GAME_SIGNAL = this.parSheet.actions.diamondWheelGame;

// Signal Handler on Client side
handle_signal: function( msg ) {
        switch( msg.protocol ) {
            case SIG.DIAMOND_WHEEL_GAME_SIGNAL: {
                ...
            }
                break;
            ...
```

> Error Response

```json
```

### 1번 Response Parameters

Parameter | Default | Description
--------- | ------- | -----------
rand | int(0-7) | 다이아몬드 프리스핀휠 스트립의 랜드값
result | int(1-30) | 다이아몬드 프리스핀휠 스트립의 결과값

> 1번 Response

```json
{
    "protocol": 120,
    "action": 1,
    "code": 200,
    "nextStep":1,
    "rand":4,
    "result":11
}
```

> Error Response

```json
```

### 2번 Response Parameters

Parameter | Default | Description
--------- | ------- | -----------
rand | int(0-7) | 다이아몬드 릴 어레이 휠의 랜드값
result | string | 다이아몬드 릴 어레이 휠의 결과값

> 2번 Response

```json
{
    "protocol": 120,
    "action": 1,
    "code": 200,
    "nextStep":2,
    "rand":5,
    "result":"R4"
}
```

> Error Response

```json
```

### 3번 Response Parameters

Parameter | Default | Description
--------- | ------- | -----------
rand | int(0-7) | 다이아몬드휠 와일드 릴 스트립의 랜드값
result | object | 다이아몬드휠 게임의 결과값이 들어있는 오브젝트
wheelStep1 | string | 다이아몬드휠 릴 어레이 스트립의 결과값
wheelStep2 | string | 다이아몬드휠 와일드 릴 스트립의 결과값
clientSetting | object | 클라이언트 세팅을 위한 파싱 결과가 담긴 오브젝트
reelArray | int(1-4) | (클라이언트에서) 세팅해야할 캣휠 릴 어레이 갯수
wildReels | int Array(0-5) | (클라이언트에서) 세팅해야할 와일드 스트립(와일드로 가득찬) 인덱스( 0이면 첫번째, 4이면 5번째 릴 )
remainSpinCount | int(1-max) | (클라이언트에서) 세팅해야할 프리스핀 횟수
nextStrip | int Array(스트립길이x5) | 다음번 다이아몬드스핀시 돌릴 스트립들(모든 릴 어레이 공통)

> 3번 Response

```json
{
    "protocol": 120,
    "action": 1,
    "code": 200,
    "nextStep":-1,
    "rand":3,
    "result":{
        "wheelStep1":"R4",
        "wheelStep2":"W15",
        "clientSetting":{
            "reelArray":4,
            "wildReels":[0,4]
        },
        "remainSpinCount":11,
        "nextStrip":[
            [23,23,23,23,23,23,23,23,23,23,23,23,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
            [23,23,23,23,23,23,23,23,23,23,23,23,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
            [23,23,23,23,23,23,23,23,23,23,23,23,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
            [23,23,23,23,23,23,23,23,23,23,23,23,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
            [23,23,23,23,23,23,23,23,23,23,23,23,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14]
        ]
    }
}
```

> Error Response

```json
```

## Super Diamond Wheel Game

총 `4`번의 Request를 서버로 보냄.
1. 프리스핀휠에 더해질 횟수 어레이 요청
2. 프리스핀 횟수 요청
3. 릴어레이 갯수 요청
4. 와일드릴의 갯수 요청 -> 모든 결과를 보냄

### 공통 Response Parameters

Parameter | Default | Description
--------- | ------- | -----------
protocol | int(120) | SIG_SLOT_CUSTOM_ACTION
action | int(2) | 파시트에서 받아온 상수
code | int(200) | 서버 OK 리스폰스 넘버
nextStep | int(-1 or 1-3) | 남은 휠게임 스텝의 리퀘스트 인덱스 넘버(-1이면 휠게임의 종료)

> Request (1-4번 모두 동일)    

```javascript
// Define Signal From parSheet
var SIG.SUPER_DIAMOND_WHEEL_GAME_SIGNAL = this.parSheet.actions.superDiamondWheelGame;

// Signal Handler on Client side
handle_signal: function( msg ) {
        switch( msg.protocol ) {
            case SIG.SUPER_DIAMOND_WHEEL_GAME_SIGNAL: {
                ...
            }
                break;
            ...
```

> Error Response

```json
```

### 1번 Response Parameters

Parameter | Default | Description
--------- | ------- | -----------
rand | int(0-7) | 슈퍼다이아몬드 프리스핀휠에 더해질 횟수의 랜드값(클라이언트에서 안쓰임)
result | int Array(8) | 슈퍼다이아몬드 프리스핀휠 Wedge에 각각 더해질 횟수들이 들어있는 결과 Array

> 1번 Response

```json
{
    "protocol": 120,
    "action": 2,
    "code": 200,
    "nextStep":1,
    "rand":0,
    "result":[0,0,0,0,0,0,0,1]
}
```

> Error Response

```json
```

### 2번 Response Parameters

Parameter | Default | Description
--------- | ------- | -----------
rand | int(0-7) | 슈퍼다이아몬드 프리스핀휠 스트립의 랜드값
result | int(1-30) | 슈퍼다이아몬드 프리스핀휠 스트립의 결과값

> 2번 Response

```json
{
    "protocol": 120,
    "action": 2,
    "code": 200,
    "nextStep":2,
    "rand":4,
    "result":11
}
```

> Error Response

```json
```

### 3번 Response Parameters

Parameter | Default | Description
--------- | ------- | -----------
rand | int(0-7) | 슈퍼다이아몬드 릴 어레이 휠의 랜드값
result | string | 슈퍼다이아몬드 릴 어레이 휠의 결과값

> 3번 Response

```json
{
    "protocol": 120,
    "action": 2,
    "code": 200,
    "nextStep":2,
    "rand":0,
    "result":"R2"
}
```

> Error Response

```json
```

### 4번 Response Parameters

Parameter | Default | Description
--------- | ------- | -----------
rand | int(0-7) | 슈퍼다이아몬드 와일드 릴 스트립의 랜드값
result | object | 슈퍼다이아몬드휠 게임의 결과값이 들어있는 오브젝트
wheelStep1 | string | 슈퍼다이아몬드휠 릴 어레이 스트립의 결과값
wheelStep2 | string | 슈퍼다이아몬드휠 릴 어레이 스트립의 결과값
wheelStep3 | string | 슈퍼다이아몬드휠 와일드 릴 스트립의 결과값
clientSetting | object | 클라이언트 세팅을 위한 파싱 결과가 담긴 오브젝트
reelArray | int(1-4) | (클라이언트에서) 세팅해야할 캣휠 릴 어레이 갯수
wildReels | int Array(0-5) | (클라이언트에서) 세팅해야할 와일드 스트립(와일드로 가득찬) 인덱스( 0이면 첫번째, 4이면 5번째 릴 )
remainSpinCount | int(1-max) | (클라이언트에서) 세팅해야할 프리스핀 횟수
nextStrip | int Array(스트립길이x5) | 다음번 슈퍼다이아몬드스핀시 돌릴 스트립들(모든 릴 어레이 공통)

> 4번 Response

```json
{
    "protocol": 120,
    "action": 2,
    "code": 200,
    "nextStep":-1,
    "rand":1,
    "result":{
        "wheelStep1":[0,0,0,0,0,0,0,1],
        "wheelStep2":"R2",
        "wheelStep3":"W13",
        "clientSetting":{
            "reelArray":2,
            "wildReels":[0,2]
        },
        "remainSpinCount":11,
        "nextStrip":[
            [21,21,21,21,21,21,21,21,21,21,21,21,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
            [21,21,21,21,21,21,21,21,21,21,21,21,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
            [21,21,21,21,21,21,21,21,21,21,21,21,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
            [21,21,21,21,21,21,21,21,21,21,21,21,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
            [21,21,21,21,21,21,21,21,21,21,21,21,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14]
        ]
    }
}
```

> Error Response

```json
```

## FreeSpin
`Cat Wheel Game` 결과를 기반으로 프리스핀 진행

<aside class="success">
Remember — `FreeSpin`, `Diamond Spin`, `Super Diamond Spin`은 기본적으로 같은 구조의 리스폰스를 보냄
</aside>

> Request      

```javascript
// Define Signal From parSheet
var SIG.FREESPIN_GAME_SIGNAL = this.parSheet.actions.freeSpinGame;

// Signal Handler on Client side
handle_signal: function( msg ) {
        switch( msg.protocol ) {
            case SIG.FREESPIN_GAME_SIGNAL: {
                ...
            }
                break;
            ...
```

### Response Parameters

Parameter | Default | Description
--------- | ------- | -----------
protocol | int(120) | SIG_SLOT_CUSTOM_ACTION
action | int(3) | 파시트에서 받아온 상수
code | int(200) | 서버 OK 리스폰스 넘버
rands | int Array(5x릴어레이갯수) | 릴어레이 갯수 만큼의 랜드값
result | object Array(당첨항목수x릴어레이갯수) | 각 릴어레이의 획득 결과 내용이 담긴 어레이
reelArrayWins | int Array(릴어레이갯수) | 릴 어레이별로 획득한 총 금액(result의 합산)
reelArrayJackpots | boolean | 릴 어레이별 잭팟 당첨 여부
freeSpinTotalWin | 프리스핀 중의 총 획득 금액
remainSpinCount | 현재 남은 스핀 횟수
wildReelIdxArr | int Array(1-4) | 캣휠피쳐에서 당첨된 와일드로 가득찬(잠긴) 어레이의 인덱스가 담긴 배열(ex: `[0]`이면 각 릴 어레이의 1번째 릴이 와일드로 잠김)
nextStrip | int Array(스트립길이x5) | 다음번 스핀시 돌릴 스트립들

### Response Parameters in DEBUG

Parameter | Default | Description
--------- | ------- | -----------
DEBUG_FOR_CLIENT_GRID | int Array(5x4) Array(릴어레이갯수) | 랜드한 그리드 결과

> Response

```json
{
    "protocol": 120,
    "action": 3,
    "code": 200,
    "rands":[[3,29,19,3,21],[14,18,24,52,22]],
    "result":[
        [],
        [
            {"win":4,"matchSymbolID":16,"name":"CushionMajor","matchCount":3,"lineIndex":1,"wildCount":2},
            {"win":4,"matchSymbolID":15,"name":"RingMajor","matchCount":3,"lineIndex":4,"wildCount":2},
            {"win":4,"matchSymbolID":16,"name":"CushionMajor","matchCount":3,"lineIndex":8,"wildCount":2},
            {"win":4,"matchSymbolID":21,"name":"SpadeMinor","matchCount":3,"lineIndex":11,"wildCount":3},
            {"win":4,"matchSymbolID":15,"name":"RingMajor","matchCount":3,"lineIndex":14,"wildCount":2},
            {"win":4,"matchSymbolID":21,"name":"SpadeMinor","matchCount":3,"lineIndex":19,"wildCount":2},
            {"win":4,"matchSymbolID":21,"name":"SpadeMinor","matchCount":3,"lineIndex":20,"wildCount":2},
            {"win":4,"matchSymbolID":16,"name":"CushionMajor","matchCount":3,"lineIndex":23,"wildCount":2},
            {"win":4,"matchSymbolID":15,"name":"RingMajor","matchCount":3,"lineIndex":26,"wildCount":3},
            {"win":4,"matchSymbolID":16,"name":"CushionMajor","matchCount":3,"lineIndex":30,"wildCount":3},
            {"win":4,"matchSymbolID":21,"name":"SpadeMinor","matchCount":3,"lineIndex":33,"wildCount":2},
            {"win":4,"matchSymbolID":15,"name":"RingMajor","matchCount":3,"lineIndex":36,"wildCount":3},
            {"win":4,"matchSymbolID":21,"name":"SpadeMinor","matchCount":3,"lineIndex":41,"wildCount":2},
            {"win":4,"matchSymbolID":21,"name":"SpadeMinor","matchCount":3,"lineIndex":42,"wildCount":2},
            {"win":4,"matchSymbolID":16,"name":"CushionMajor","matchCount":3,"lineIndex":45,"wildCount":3},
            {"win":4,"matchSymbolID":21,"name":"SpadeMinor","matchCount":3,"lineIndex":49,"wildCount":2}
        ]
    ],
    "reelArrayWins":[0,64],
    "reelArrayJackpots":[false,false],
    "freeSpinTotalWin":426,
    "remainSpinCount":3,
    "wildReelIdxArr":[0],
    "nextStrip":[
        [23,23,23,23,23,23,23,23,23,23,23,23,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
        [23,23,23,23,23,23,23,23,23,23,23,23,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
        [23,23,23,23,23,23,23,23,23,23,23,23,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
        [23,23,23,23,23,23,23,23,23,23,23,23,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
        [23,23,23,23,23,23,23,23,23,23,23,23,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14]
    ],
    "DEBUG_FOR_CLIENT_GRID":[
        [
            [1,15,90,13,23],[1,16,1,14,24],[1,21,11,12,90],[1,22,12,12,1]
        ],[
            [1,15,90,13,23],[1,16,1,14,24],[1,21,11,12,90],[1,22,12,12,1]
        ]
    ]
}
```

> Response on Jackpot

```json
{
    "protocol": 120,
    "action": 3,
    "code": 200,
    "rands":[[3,13,19,22,21],[14,18,42,32,22]],
    "result":[
        [
            {"win":80000,"name":"Jackpot","matchSymbolID":1,"matchCount":50,"wildCount":50}
        ],
        [
            {"win":80000,"name":"Jackpot","matchSymbolID":1,"matchCount":50,"wildCount":50}
        ]
    ],
    "reelArrayWins":[80000,80000],
    "reelArrayJackpots":[true,true],
    "freeSpinTotalWin":160000,
    "remainSpinCount":5,
    "wildReelIdxArr":[0],
    "nextStrip":[
        [23,23,23,23,23,23,23,23,23,23,23,23,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
        [23,23,23,23,23,23,23,23,23,23,23,23,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
        [23,23,23,23,23,23,23,23,23,23,23,23,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
        [23,23,23,23,23,23,23,23,23,23,23,23,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
        [23,23,23,23,23,23,23,23,23,23,23,23,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14]
    ],
    "DEBUG_FOR_CLIENT_GRID":[
        [
            [1,1,1,1,1],[1,1,1,1,1],[1,1,1,1,1],[1,1,1,1,1]
        ],[
            [1,1,1,1,1],[1,1,1,1,1],[1,1,1,1,1],[1,1,1,1,1]
        ]
    ]
}
```

> Error Response

```json
```

## Diamond Spin
`Diamond Wheel Game` 결과를 기반으로 프리스핀 진행

<aside class="success">
Remember — `FreeSpin`, `Diamond Spin`, `Super Diamond Spin`은 기본적으로 같은 구조의 리스폰스를 보냄
</aside>

> Request      

```javascript
// Define Signal From parSheet
var SIG.DIAMOND_SPIN_GAME_SIGNAL = this.parSheet.actions.diamondSpinGame;

// Signal Handler on Client side
handle_signal: function( msg ) {
        switch( msg.protocol ) {
            case SIG.DIAMOND_SPIN_GAME_SIGNAL: {
                ...
            }
                break;
            ...
```

### Response Parameters

Parameter | Default | Description
--------- | ------- | -----------
protocol | int(120) | SIG_SLOT_CUSTOM_ACTION
action | int(4) | 파시트에서 받아온 상수
code | int(200) | 서버 OK 리스폰스 넘버
rands | int Array(5x릴어레이갯수) | 릴어레이 갯수 만큼의 랜드값
result | object Array(당첨항목수x릴어레이갯수) | 각 릴어레이의 획득 결과 내용이 담긴 어레이
reelArrayWins | int Array(릴어레이갯수) | 릴 어레이별로 획득한 총 금액(result의 합산)
reelArrayJackpots | boolean | 릴 어레이별 잭팟 당첨 여부
freeSpinTotalWin | 프리스핀 중의 총 획득 금액
remainSpinCount | 현재 남은 스핀 횟수
wildReelIdxArr | int Array(1-4) | 다이아몬드휠피쳐에서 당첨된 와일드로 가득찬(잠긴) 어레이의 인덱스가 담긴 배열(ex: `[0]`이면 각 릴 어레이의 1번째 릴이 와일드로 잠김)
nextStrip | int Array(스트립길이x5) | 다음번 스핀시 돌릴 스트립들

### Response Parameters in DEBUG

Parameter | Default | Description
--------- | ------- | -----------
DEBUG_FOR_CLIENT_GRID | int Array(5x4) Array(릴어레이갯수) | 랜드한 그리드 결과

> Response

```json
{
    "protocol": 120,
    "action":4,
    "code":200,
    "rands":[[41,33,48,24,19],[36,42,40,12,19]],
    "result":[
        [
            {"win":10,"matchSymbolID":23,"name":"CloverMinor","matchCount":4,"lineIndex":1,"wildCount":3},
            {"win":4,"matchSymbolID":22,"name":"HeartMinor","matchCount":3,"lineIndex":4,"wildCount":2},
            {"win":10,"matchSymbolID":23,"name":"CloverMinor","matchCount":4,"lineIndex":8,"wildCount":3},
            {"win":4,"matchSymbolID":24,"name":"DiamondMinor","matchCount":3,"lineIndex":11,"wildCount":2},
            {"win":4,"matchSymbolID":22,"name":"HeartMinor","matchCount":3,"lineIndex":14,"wildCount":2},
            {"win":4,"matchSymbolID":24,"name":"DiamondMinor","matchCount":3,"lineIndex":19,"wildCount":2},
            {"win":4,"matchSymbolID":24,"name":"DiamondMinor","matchCount":3,"lineIndex":20,"wildCount":2},
            {"win":10,"matchSymbolID":23,"name":"CloverMinor","matchCount":4,"lineIndex":23,"wildCount":3},
            {"win":4,"matchSymbolID":22,"name":"HeartMinor","matchCount":3,"lineIndex":26,"wildCount":2},
            {"win":4,"matchSymbolID":23,"name":"CloverMinor","matchCount":3,"lineIndex":30,"wildCount":2},
            {"win":4,"matchSymbolID":24,"name":"DiamondMinor","matchCount":3,"lineIndex":33,"wildCount":2},
            {"win":4,"matchSymbolID":22,"name":"HeartMinor","matchCount":3,"lineIndex":36,"wildCount":2},
            {"win":4,"matchSymbolID":24,"name":"DiamondMinor","matchCount":3,"lineIndex":41,"wildCount":2},
            {"win":4,"matchSymbolID":24,"name":"DiamondMinor","matchCount":3,"lineIndex":42,"wildCount":2},
            {"win":4,"matchSymbolID":23,"name":"CloverMinor","matchCount":3,"lineIndex":45,"wildCount":2},
            {"win":4,"matchSymbolID":24,"name":"DiamondMinor","matchCount":3,"lineIndex":49,"wildCount":2}
        ],
        []
    ],
    "reelArrayWins":[82,0],
    "reelArrayJackpots":[false,false],
    "freeSpinTotalWin":4290,
    "remainSpinCount":2,
    "wildReelIdxArr":[0],
    "nextStrip":[
        [12,12,12,12,12,12,12,12,12,12,12,12,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
        [12,12,12,12,12,12,12,12,12,12,12,12,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
        [12,12,12,12,12,12,12,12,12,12,12,12,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
        [12,12,12,12,12,12,12,12,12,12,12,12,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
        [12,12,12,12,12,12,12,12,12,12,12,12,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14]
    ],
    "DEBUG_FOR_CLIENT_GRID":[
        [
            [1,15,13,23,16],[1,16,14,1,21],[1,21,15,11,22],[1,22,16,12,23]
        ],[
            [1,15,13,23,16],[1,16,14,1,21],[1,21,15,11,22],[1,22,16,12,23]
        ]
    ]
}
```

> Response on Jackpot

```json
{
    "protocol": 120,
    "action": 4,
    "code": 200,
    "rands":[[11,33,23,24,19],[23,32,32,12,19]],
    "result":[
        [
            {"win":80000,"name":"Jackpot","matchSymbolID":1,"matchCount":50,"wildCount":50}
        ],
        [
            {"win":80000,"name":"Jackpot","matchSymbolID":1,"matchCount":50,"wildCount":50}
        ]
    ],
    "reelArrayWins":[80000,80000],
    "reelArrayJackpots":[true,true],
    "freeSpinTotalWin":160000,
    "remainSpinCount":7,
    "wildReelIdxArr":[0],
    "nextStrip":[
        [23,23,23,23,23,23,23,23,23,23,23,23,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
        [23,23,23,23,23,23,23,23,23,23,23,23,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
        [23,23,23,23,23,23,23,23,23,23,23,23,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
        [23,23,23,23,23,23,23,23,23,23,23,23,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
        [23,23,23,23,23,23,23,23,23,23,23,23,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14]
    ],
    "DEBUG_FOR_CLIENT_GRID":[
        [
            [1,1,1,1,1],[1,1,1,1,1],[1,1,1,1,1],[1,1,1,1,1]
        ],[
            [1,1,1,1,1],[1,1,1,1,1],[1,1,1,1,1],[1,1,1,1,1]
        ]
    ]
}
```

> Error Response

```json
```

## Super Diamond Spin
`Super Diamond Wheel Game` 결과를 기반으로 프리스핀 진행

<aside class="success">
Remember — `FreeSpin`, `Diamond Spin`, `Super Diamond Spin`은 기본적으로 같은 구조의 리스폰스를 보냄
</aside>

> Request      

```javascript
// Define Signal From parSheet
var SIG.SUPER_DIAMOND_SPIN_GAME_SIGNAL = this.parSheet.actions.superDiamondSpinGame;

// Signal Handler on Client side
handle_signal: function( msg ) {
        switch( msg.protocol ) {
            case SIG.SUPER_DIAMOND_SPIN_GAME_SIGNAL: {
                ...
            }
                break;
            ...
```

### Response Parameters

Parameter | Default | Description
--------- | ------- | -----------
protocol | int(120) | SIG_SLOT_CUSTOM_ACTION
action | int(5) | 파시트에서 받아온 상수
code | int(200) | 서버 OK 리스폰스 넘버
rands | int Array(5x릴어레이갯수) | 릴어레이 갯수 만큼의 랜드값
result | object Array(당첨항목수x릴어레이갯수) | 각 릴어레이의 획득 결과 내용이 담긴 어레이
reelArrayWins | int Array(릴어레이갯수) | 릴 어레이별로 획득한 총 금액(result의 합산)
reelArrayJackpots | boolean | 릴 어레이별 잭팟 당첨 여부
freeSpinTotalWin | 프리스핀 중의 총 획득 금액
remainSpinCount | 현재 남은 스핀 횟수
wildReelIdxArr | int Array(1-4) | 다이아몬드휠피쳐에서 당첨된 와일드로 가득찬(잠긴) 어레이의 인덱스가 담긴 배열(ex: `[0]`이면 각 릴 어레이의 1번째 릴이 와일드로 잠김)
nextStrip | int Array(스트립길이x5) | 다음번 스핀시 돌릴 스트립들

### Response Parameters in DEBUG

Parameter | Default | Description
--------- | ------- | -----------
DEBUG_FOR_CLIENT_GRID | int Array(5x4) Array(릴어레이갯수) | 랜드한 그리드 결과

> Response

```json
{
    "protocol": 120,
    "action":5,
    "code":200,
    "rands":[[17,6,14,1,30],[2,41,43,29,10]],
    "result":[[],[]],
    "reelArrayWins":[0,0],
    "reelArrayJackpots":[false,false],
    "freeSpinTotalWin":972,
    "remainSpinCount":1,
    "wildReelIdxArr":[0],
    "nextStrip":[
        [15,15,15,90,90,90,90,90,15,15,15,15,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
        [15,15,15,90,90,90,90,90,15,15,15,15,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
        [15,15,15,90,90,90,90,90,15,15,15,15,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
        [15,15,15,90,90,90,90,90,15,15,15,15,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
        [15,15,15,90,90,90,90,90,15,15,15,15,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14]
    ],
    "DEBUG_FOR_CLIENT_GRID":[
        [
            [1,14,16,14,24],[1,15,21,15,24],[1,16,22,16,24],[1,21,23,21,1]
        ],[
            [1,14,16,14,24],[1,15,21,15,24],[1,16,22,16,24],[1,21,23,21,1]
        ]
    ]
}
```

> Response on Jackpot

```json
{
    "protocol": 120,
    "action": 5,
    "code": 200,
    "rands":[[11,22,44,24,19],[23,32,32,12,19]],
    "result":[
        [
            {"win":80000,"name":"Jackpot","matchSymbolID":1,"matchCount":50,"wildCount":50}
        ],
        [
            {"win":80000,"name":"Jackpot","matchSymbolID":1,"matchCount":50,"wildCount":50}
        ]
    ],
    "reelArrayWins":[80000,80000],
    "reelArrayJackpots":[true,true],
    "freeSpinTotalWin":160000,
    "remainSpinCount":7,
    "wildReelIdxArr":[0],
    "nextStrip":[
        [23,23,23,23,23,23,23,23,23,23,23,23,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
        [23,23,23,23,23,23,23,23,23,23,23,23,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
        [23,23,23,23,23,23,23,23,23,23,23,23,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
        [23,23,23,23,23,23,23,23,23,23,23,23,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14],
        [23,23,23,23,23,23,23,23,23,23,23,23,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14,15,16,21,22,23,24,90,1,11,12,13,14]
    ],
    "DEBUG_FOR_CLIENT_GRID":[
        [
            [1,1,1,1,1],[1,1,1,1,1],[1,1,1,1,1],[1,1,1,1,1]
        ],[
            [1,1,1,1,1],[1,1,1,1,1],[1,1,1,1,1],[1,1,1,1,1]
        ]
    ]
}
```

> Error Response

```json
```

# Protocols

<aside class="notice">
프로토콜 문서
</aside>

Slot No.82 Diamond Cats

Code | Meaning | Argument
---------- | ------- | -------
0 | catWheelGame | None
1 | diamondWheelGame | None
2 | superDiamondWheelGame | None
3 | freeSpinGame | None
4 | diamondSpinGame | None
5 | superDiamondSpinGame | None
