---
title: Slot No.85 LunarFortune Message Protocols

language_tabs: # must be one of https://git.io/vQNgJ
  - json

toc_footers:
  - <a href='https://alansynn.com'>Documented by Alan Synn</a>
  - Rev 1.0

includes:
  - slot

search: true
---

# Slot No.85 LunarFortune 메시지 프로토콜 소개 문서
### Rev 1.1
이하 호출 프로토콜에서 기본으로 필요한 `SIG_SLOT protocol`은 설명에서 제외.

## 수정내역
### Rev 1
2019-06-12 18:00 

+ 기본사항

### Rev 1.1
2019-06-19 11:55

+ PickGame Result 패킷에 프리스핀 횟수 추가

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
> 상대적으로 긴 정보는 ... 으로 표시. 상세사항은 Argument 탭 참조.

```json
{
    "code": 200,
    "gameID": 85,
    "rid": 0,
    "gameInfo": {
        "betTable": [ 2, 5, 10, 25, 50, 75, 60000 ],
        "betLimit": [ { "level": 2, "bet": 20000 }, { "level": 6, "bet": 40000 }, { "level": 9, "bet": 80000 } ],
        "betIndex": -1,
        "betLines": 9,
        "betPerLine": 10,
        "parSheet": {
            "TEST_MODE": false,
            "betTable": [ 100, 200, 500, 1000, 2000, 4000, 8000, 20000, 40000, 80000, 200000, 400000, 800000, 2000000, 4000000, 8000000, 20000000, 40000000 ],
            "payLines": [ "0x111", "0x000", "0x222", "0x012", "0x210", "0x101", "0x121", "0x212", "0x010" ],
            "symbols": [
                { "id": 71, "name": "NoSymbol", "type": 0, "typifyName": "lfSymEmptyAR" },
                { "id": 11, "name": "Gold", "type": 0, "typifyName": "lfSymMajor01_GoldAR" },
                { "id": 1, "name": "Wild01", "type": 0, "typifyName": "lfSymWild02_x1AR" },
                { "id": 2, "name": "Wild02", "type": 0, "typifyName": "lfSymWild01_x2AR" },
                { "id": 41, "name": "GrandJackpot", "type": 0, "typifyName": "lfSymScatter01_GrandAR" },
                { "id": 42, "name": "MegaJackpot", "type": 0, "typifyName": "lfSymScatter01_MegaAR" },
                { "id": 43, "name": "MajorJackpot", "type": 0, "typifyName": "lfSymScatter01_MajorAR" },
                { "id": 44, "name": "MinorJackpot", "type": 0, "typifyName": "lfSymScatter01_MinorAR" },
                { "id": 50, "name": "Direct", "type": 0, "typifyName": "lfSymScatter02_DirectpayAR", "value": 0.5 },
                { "id": 51, "name": "Direct", "type": 0, "typifyName": "lfSymScatter02_DirectpayAR", "value": 1 },
                { "id": 52, "name": "Direct", "type": 0, "typifyName": "lfSymScatter02_DirectpayAR", "value": 1.5 },
                { "id": 53, "name": "Direct", "type": 0, "typifyName": "lfSymScatter02_DirectpayAR", "value": 2 },
                { "id": 54, "name": "Direct", "type": 0, "typifyName": "lfSymScatter02_DirectpayAR", "value": 2.5 },
                { "id": 13, "name": "Seven", "type": 0, "typifyName": "lfSymMajor03_7AR" },
                { "id": 12, "name": "SevenSevenSeven", "type": 0, "typifyName": "lfSymMajor02_777AR" },
                { "id": 21, "name": "Bar03", "type": 0, "typifyName": "lfSymMinor01_3barAR" },
                { "id": 22, "name": "Bar02", "type": 0, "typifyName": "lfSymMinor02_2barAR" },
                { "id": 23, "name": "Bar01", "type": 0, "typifyName": "lfSymMinor03_1barAR" }
            ],
            "linkSymbols": [
                { "id": 99, "name": "Lunar", "type": 0, "typifyName": "lfSymScatter03_LunarLinkAR" },
                { "id": 11, "name": "Gold", "type": 0, "typifyName": "lfSymMajor01_Gold_LinkAR" },
                { "id": 1, "name": "Wild01", "type": 0, "typifyName": "lfSymWild02_x1_LinkAR" },
                { "id": 2, "name": "Wild02", "type": 0, "typifyName": "lfSymWild01_x2_LinkAR" },
                { "id": 41, "name": "GrandJackpot", "type": 0, "typifyName": "lfSymScatter01_Grand_LinkAR" },
                { "id": 42, "name": "MegaJackpot", "type": 0, "typifyName": "lfSymScatter01_Mega_LinkAR" },
                { "id": 43, "name": "MajorJackpot", "type": 0, "typifyName": "lfSymScatter01_Major_LinkAR" },
                { "id": 44, "name": "MinorJackpot", "type": 0, "typifyName": "lfSymScatter01_Minor_LinkAR" },
                { "id": 50, "name": "Direct", "type": 0, "typifyName": "lfSymScatter02_DirectpayLinkAR", "value": 0.5 },
                { "id": 51, "name": "Direct", "type": 0, "typifyName": "lfSymScatter02_Directpay_linkAR", "value": 1 },
                { "id": 52, "name": "Direct", "type": 0, "typifyName": "lfSymScatter02_Directpay_linkAR", "value": 1.5 },
                { "id": 53, "name": "Direct", "type": 0, "typifyName": "lfSymScatter02_Directpay_linkAR", "value": 2 },
                { "id": 54, "name": "Direct", "type": 0, "typifyName": "lfSymScatter02_Directpay_linkAR", "value": 2.5 },
                { "id": 13, "name": "Seven", "type": 0, "typifyName": "lfSymMajor03_7_linkAR" },
                { "id": 12, "name": "SevenSevenSeven", "type": 0, "typifyName": "lfSymMajor02_777_LinkAR" },
                { "id": 21, "name": "Bar03", "type": 0, "typifyName": "lfSymMinor01_3bar_LinkAR" },
                { "id": 22, "name": "Bar02", "type": 0, "typifyName": "lfSymMinor02_2bar_LinkAR" },
                { "id": 23, "name": "Bar01", "type": 0, "typifyName": "lfSymMinor03_1bar_LinkAR" }
            ],
            "reels": [
                {
                    "index": 0,
                    "strip": [ 71, 41, 71, 42, 71, 43, 71, 44, 71, 50, 71, 51, 71, 52, 71, 53, 71, 54, 71, 1, 71, 2, 71, 11, 71, 12, 71, 13, 71, 21, 71, 22, 71, 23 ]
                },
                {
                    "index": 1,
                    "strip": [ 71, 41, 71, 42, 71, 43, 71, 44, 71, 50, 71, 51, 71, 52, 71, 53, 71, 54, 71, 1, 71, 2, 71, 11, 71, 12, 71, 13, 71, 21, 71, 22, 71, 23 ]
                },
                {
                    "index": 2,
                    "strip": [ 71, 41, 71, 42, 71, 43, 71, 44, 71, 50, 71, 51, 71, 52, 71, 53, 71, 54, 71, 1, 71, 2, 71, 11, 71, 12, 71, 13, 71, 21, 71, 22, 71, 23 ]
                }
            ],
            "blueLinkReels": [
                {
                    "index": 0,
                    "strip": [ 41, 1, 42, 2, 43, 12, 44, 13, 50, 21, 51, 22, 52, 23, 54, 11, 13 ]
                },
                {
                    "index": 1,
                    "strip": [ 41, 1, 42, 2, 43, 12, 44, 13, 50, 21, 51, 22, 52, 23, 54, 11, 13 ]
                },
                {
                    "index": 2,
                    "strip": [ 41, 1, 42, 2, 43, 12, 44, 13, 50, 21, 51, 22, 52, 23, 54, 11, 13 ]
                },
                {
                    "index": 3,
                    "strip": [ 41, 1, 42, 2, 43, 12, 44, 13, 50, 21, 51, 22, 52, 23, 54, 11, 13 ]
                },
                {
                    "index": 4,
                    "strip": [ 41, 1, 42, 2, 43, 12, 44, 13, 50, 21, 51, 22, 52, 23, 54, 11, 13 ]
                },
                {
                    "index": 5,
                    "strip": [ 41, 1, 42, 2, 43, 12, 44, 13, 50, 21, 51, 22, 52, 23, 54, 11, 13 ]
                },
                {
                    "index": 6,
                    "strip": [ 41, 1, 42, 2, 43, 12, 44, 13, 50, 21, 51, 22, 52, 23, 54, 11, 13 ]
                },
                {
                    "index": 7,
                    "strip": [ 41, 1, 42, 2, 43, 12, 44, 13, 50, 21, 51, 22, 52, 23, 54, 11, 13 ]
                },
                {
                    "index": 8,
                    "strip": [ 41, 1, 42, 2, 43, 12, 44, 13, 50, 21, 51, 22, 52, 23, 54, 11, 13 ]
                }
            ],
            "redLinkReels": [
                {
                    "index": 0,
                    "strip": [ 41, 1, 42, 2, 43, 12, 44, 13, 50, 21, 51, 22, 52, 23, 54, 11, 13 ]
                },
                {
                    "index": 1,
                    "strip": [ 41, 1, 42, 2, 43, 12, 44, 13, 50, 21, 51, 22, 52, 23, 54, 11, 13 ]
                },
                {
                    "index": 2,
                    "strip": [ 41, 1, 42, 2, 43, 12, 44, 13, 50, 21, 51, 22, 52, 23, 54, 11, 13 ]
                },
                {
                    "index": 3,
                    "strip": [ 41, 1, 42, 2, 43, 12, 44, 13, 50, 21, 51, 22, 52, 23, 54, 11, 13 ]
                }, ...총 18개 (index : 0 - 17)
            ],
            "highBalanceFreeSpinProb": [ 0.98, 0.96, 0.76, 0.5 ],
            "x1WildSymbolID": 1,
            "x2WildSymbolID": 2,
            "wildSymbolIDs": [ 1, 2 ],
            "wildMultiply": [ 1, 2 ],
            "linkTriggerSymbolIDs": [ 41, 42, 43, 44, 50, 51, 52, 53, 54 ],
            "majorSymbolIDs": [ 11, 12, 13, 21, 22, 23 ],
            "scatterSymbolIDs": [ 31, 41 ],
            "linkSymbolIDs": [ 99, 54, 53, 52, 51, 50, 44, 43, 42, 41, 11 ],
            "lunarSymbolID": 99,
            "goldSymbolID": 11,
            "linkJackpotSymbolIDs": [ 44, 43, 42, 41 ],
            "linkDirectSymbolIDs": [ 54, 53, 52, 51, 50 ],
            "noSymbolID": 71,
            "actions": { "pickGame": 0, "blueLinkSpin": 1, "redLinkSpin": 2, "claimResultWin": 3 }
        },
        "maxLine": 9
    },
    "gameName": "lunarFortune",
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
rands | int(0-스트립길이) Array(3) | 랜드값
isPickGame | boolean | 픽게임에 당첨되었는지 여부
redOverlayArr | int(-1 or 1) Array(9) | 레드 오버레이 심볼 1d 어레이 1이면 있는것, -1이면 없는것 
blueOverlayArr | int(-1 or 1) Array(9) | 블루 오버레이 심볼 1d 어레이 1이면 있는것, -1이면 없는것 
redSymbolCount | int(0-max) | 현재(이번 스핀)까지 획득한 레드심볼 수
blueSymbolCount | int(0-max) | 현재(이번 스핀)까지 획득한 블루심볼 수
result | object Array | 획득 결과 내용
totalWin | int(0-max) | 획득 결과 금액
winInfo | object | 획득 정보에 대한 판정을 담은 객체
winInfo.isMajorWin | boolean | 메이져 윈 여부
winInfo.majorWinIndex | int(-1-4) | 메이져윈일 경우의 인덱스
winInfo.multiple | int(0-max) | 당첨금액/총배팅액 결과
winInfo.lineMultiple | int(0-max) | 당첨금액/라인배팅액 결과

### Response Parameters in DEBUG

Parameter | Default | Description
--------- | ------- | -----------
DEBUG_FOR_CLIENT_GRID | int Array(9) | 랜드한 심볼 이름

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
    "rands": [15,23,19],
    "isPickGame": false,
    "redOverlayArr": [1,-1,-1,-1,-1,-1,-1,-1,-1],
    "blueOverlayArr": [-1,-1,1,-1,-1,-1,-1,-1,-1],
    "redSymbolCount": 6,
    "blueSymbolCount": 1,
    "result": [],
    "totalWin": 0,
    "winInfo": {
        "isMajorWin": false,
        "majorWinIndex": -1,
        "multiple": 0,
        "lineMultiple": 0
    },
    "DEBUG_FOR_CLIENT_GRID": [
        [
            "NoSymbol",
            "Direct",
            "NoSymbol"
        ],
        [
            "NoSymbol",
            "Gold",
            "NoSymbol"
        ],
        [
            "NoSymbol",
            "Wild01",
            "NoSymbol"
        ]
    ]
} 
```

> Error Response

```json
```

## Pick Game

### Response Parameters

Parameter | Default | Description
--------- | ------- | -----------
protocol | int(120) | SIG_SLOT_CUSTOM_ACTION
action | int(0) | 파시트에서 받아온 상수
code | int(200) | 서버 OK 리스폰스 넘버
isRed | boolean | 레드 링크에 당첨되었는지 여부
isBlue | boolean | 블루 링크에 당첨되었는지 여부
freeSpinCount | int(1-max) | 프리스핀 횟수(ex: 8(최소 프리스핀횟수, 기본값) + 각 게임(red, blue)을 위해 획득한 심볼갯수)
result | int(-1 or 1) Array(3) | 0번 인덱스가 유저가 고른 결과, 나머지는 셔플된 결과. 1이면 Red Link이고 -1 이면 Blue Link

> Request  
Spin 요청

```javascript
// Define Pick Game Signal From parSheet
var SIG.PICK_GAME_SIGNAL = this.parSheet.actions.pickGame;

// Signal Handler on Client side
handle_signal: function( msg ) {
        switch( msg.protocol ) {
            case SIG.PICK_GAME_SIGNAL: {
                ...
            }
                break;
            ...
```

> Response

```json
{
    "protocol": 120,
    "action": 0,
    "code": 200,
    "isRed": true,
    "isBlue": false,
    "freeSpinCount": 8,
    "result": [1,-1,-1],
    
}
```

> Error Response

```json
```


## Blue Link Game

### Response Parameters

Parameter | Default | Description
--------- | ------- | -----------
protocol | int(120) | SIG_SLOT_CUSTOM_ACTION
action | int(1) | 파시트에서 받아온 상수
code | int(200) | 서버 OK 리스폰스 넘버
rands | int Array(9) | 그리드 전체의 랜드값
blueLinkSpinCount | int(0-100) | 남은 블루링크 스핀수
totalWin | int(0-max) | 획득 금액
jackpot | boolean | 잭팟 여부
jackpotWin | int(0-max) | 잭팟으로 획득한 금액 
directWin | int(0-max) | 다이렉트페이로 획득한 금액

### Response Parameters in DEBUG

Parameter | Default | Description
--------- | ------- | -----------
DEBUG_FOR_CLIENT_SYMBOL_NUM_ARR | int Array(9) | 랜드한 심볼 ID값
DEBUG_FOR_CLIENT_SYMBOL_INFO_ARR | string Array(9) | 랜드한 심볼 이름

> Request  

```javascript
// Define Pick Game Signal From parSheet
var SIG.BLUE_LINK_GAME = this.parSheet.actions.blueLinkSpin;

// Signal Handler on Client side
handle_signal: function( msg ) {
        switch( msg.protocol ) {
            case SIG.BLUE_LINK_GAME: {
                ...
            }
                break;
            ...
```

> Response

```json
{
    "protocol": 120,
    "action": 1,
    "code": 200,
    "rands": [14,10,10,9,0,10,11,11,10],
    "blueLinkSpinCount": 3,
    "totalWin": 0,
    "jackpot": false,
    "jackpotWin": 0,
    "directWin": 0,
    "DEBUG_FOR_CLIENT_SYMBOL_NUM_ARR": [54,51,51,21,41,51,22,22,51],
    "DEBUG_FOR_CLIENT_SYMBOL_INFO_ARR": ["Direct","Direct","Direct","Bar03","GrandJackpot","Direct","Bar02","Bar02","Direct"]
} 
```

> Error Response

```json
```

## Red Link Game

### Response Parameters

Parameter | Default | Description
--------- | ------- | -----------
protocol | int(120) | SIG_SLOT_CUSTOM_ACTION
action | int(2) | 파시트에서 받아온 상수
code | int(200) | 서버 OK 리스폰스 넘버
rands | int Array(18) | 그리드 전체의 랜드값
redLinkSpinCount | int(0-100) | 남은 레드링크 스핀수
totalWin | int(0-max) | 얻은 금액
jackpot | boolean | 잭팟 여부
jackpotWin | int(0-max) | 잭팟으로 얻은 금액 
directWin | int(0-max) | 다이렉트페이로 얻은 금액

### Response Parameters in DEBUG

Parameter | Default | Description
--------- | ------- | -----------
DEBUG_FOR_CLIENT_SYMBOL_NUM_ARR | int Array(18) | 랜드한 심볼 ID값
DEBUG_FOR_CLIENT_SYMBOL_INFO_ARR | string Array(18) | 랜드한 심볼 이름

> Request  

```javascript
// Define Pick Game Signal From parSheet
var SIG.RED_LINK_GAME = this.parSheet.actions.redLinkSpin;

// Signal Handler on Client side
handle_signal: function( msg ) {
        switch( msg.protocol ) {
            case SIG.RED_LINK_GAME: {
                ...
            }
                break;
            ...
```

> Response

```json
{
    "protocol": 120,
    "action": 2,
    "code": 200,
    "rands": [1,14,13,15,12,0,8,13,11,13,1,12,0,3,8,7,14,9],
    "redLinkSpinCount": 3,
    "totalWin": 0,
    "jackpot": false,
    "jackpotWin": 0,
    "directWin": 0,
    "DEBUG_FOR_CLIENT_SYMBOL_NUM_ARR": [1,54,23,11,52,41,50,23,22,23,1,52,41,2,50,13,54,21],
    "DEBUG_FOR_CLIENT_SYMBOL_INFO_ARR": ["Wild01","Direct","Bar01","Gold","Direct","GrandJackpot","Direct","Bar01","Bar02","Bar01","Wild01","Direct","GrandJackpot","Wild02","Direct","Seven","Direct","Bar03"]
} 
```

> Error Response

```json
```

# Protocols

<aside class="notice">
프로토콜 문서
</aside>

Slot No.85 LunarFortune

Code | Meaning | Argument
---------- | ------- | -------
0 | Pick Game | None
1 | blueLinkSpin | None
2 | redLinkSpin | None
3 | claimResultWin | grid(1d array) index 
