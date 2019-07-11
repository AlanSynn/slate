---
title: Slot No.85 LunarFortune Message Protocols

language_tabs: # must be one of https://git.io/vQNgJ
  - json

toc_footers:
  - <a href='https://alansynn.com'>Documented by Alan Synn</a>
  - Rev 1.2

includes:
  - slot

search: true
---

# Slot No.85 LunarFortune 메시지 프로토콜 소개 문서

<p>
<div class="mermaid">
  graph LR
      A --- B
      B-->C[fa:fa-ban forbidden]
      B-->D(fa:fa-spinner);
</div>
</p>

### Rev 1.2
이하 호출 프로토콜에서 기본으로 필요한 `SIG_SLOT protocol`은 설명에서 제외.

## 수정내역
### Rev 1
2019-06-12 18:00 

+ 기본사항

### Rev 1.1
2019-06-19 11:55

+ PickGame Result 패킷에 프리스핀 횟수 추가

### Rev 1.2
2019-07-10 23:05

+ Claim Jackpot 추가
+ Phase Multiple(리프레시시 라벨 배수) 추가
+ 스핀 멈췄을때 다이렉트 페이 값 추가

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

Rev | Parameter | Default | Description
--------- | --------- | ------- | -----------
1|protocol | int(100) | SIG_SLOT_SPIN
1|code | int(200) | 서버 OK 리스폰스 넘버
1|rands | int(0-스트립길이) Array(3) | 랜드값
1|isPickGame | boolean | 픽게임에 당첨되었는지 여부
1.2|directPayInfo | int(-1-max) | 스핀 결과때 다이렉트 페이 심볼에 띄워줄 금액(row 기준)
1|redOverlayArr | int(-1 or 1) Array(9) | 레드 오버레이 심볼 1d 어레이 1이면 있는것, -1이면 없는것(row 기준)
1|blueOverlayArr | int(-1 or 1) Array(9) | 블루 오버레이 심볼 1d 어레이 1이면 있는것, -1이면 없는것(row 기준)
1.2|redSymbolCount | int(0-max) | 현재(이번 스핀)까지 획득한 레드심볼 수
1.2|blueSymbolCount | int(0-max) | 현재(이번 스핀)까지 획득한 블루심볼 수
1.2|redSymbolCountArr | int(8-max) Array(배팅인덱스 수) | 레드 심볼 카운트를 배팅금액 당 저장한 어레이
1.2|blueSymbolCountArr | int(5-max) Array(배팅인덱스 수) | 블루 심볼 카운트를 배팅금액 당 저장한 어레이
1|result | object Array | 획득 결과 내용
1|totalWin | int(0-max) | 획득 결과 금액
1|winInfo | object | 획득 정보에 대한 판정을 담은 객체
1|winInfo.isMajorWin | boolean | 메이져 윈 여부
1|winInfo.majorWinIndex | int(-1-4) | 메이져윈일 경우의 인덱스
1|winInfo.multiple | int(0-max) | 당첨금액/총배팅액 결과
1|winInfo.lineMultiple | int(0-max) | 당첨금액/라인배팅액 결과

### Response Parameters in DEBUG

Parameter | Default | Description
--------- | ------- | -----------
DEBUG_FOR_CLIENT_GRID | int Array(9) | 랜드한 심볼 이름(row 기준)
DEBUG_FOR_CLIENT_GRID_RANDS | int Array(9) | 랜드값(row 기준)

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
    "directPayInfo": [-1,450,-1,-1,-1,-1,-1,-1,-1],
    "redOverlayArr": [1,-1,-1,-1,-1,-1,-1,-1,-1],
    "blueOverlayArr": [-1,-1,1,-1,-1,-1,-1,-1,-1],
    "redSymbolCount" : 8,
    "blueSymbolCount" : 5,
    "redSymbolCountArr" : [8,8,8,8,8,8,8,8,8,8,8,8,8,8,8,8,8,8],
    "blueSymbolCountArr" : [5,5,5,5,5,5,5,5,5,5,5,5,5,5,5,5,5,5],
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
    ],
    "DEBUG_FOR_CLIENT_GRID_RANDS" : [[71,71,71],[52,21,44],[71,71,71]]
} 
```

> Error Response

```json
```

## Pick Game

### Response Parameters

Rev | Parameter | Default | Description
--------- | --------- | ------- | -----------
1|protocol | int(120) | SIG_SLOT_CUSTOM_ACTION
1|action | int(1) | 파시트에서 받아온 상수
1|code | int(200) | 서버 OK 리스폰스 넘버
1|isRed | boolean | 레드 링크에 당첨되었는지 여부
1|isBlue | boolean | 블루 링크에 당첨되었는지 여부
1|freeSpinCount | int(1-max) | 프리스핀 횟수(ex: 8(최소 프리스핀횟수, 기본값) + 각 게임(red, blue)을 위해 획득한 심볼갯수)
1|result | int(-1 or 1) Array(3) | 0번 인덱스가 유저가 고른 결과, 나머지는 셔플된 결과. 1이면 Red Link이고 -1 이면 Blue Link
1.2|isLinkMode | boolean | 링크스핀 진입 신호
1.2|randIds | int Array(9 or 18) | 랜드한 심볼의 아이디
1.2|initRands | int Array(9 or 18) | 링크스핀 씬에서 시작전에 보여줄 설정용 랜드값
1.2|winOnLock | int Array(9 or 18) | 현재 랜딩한 페이 심볼의 금액값
1.2|directPayOnLock | int Array(9 or 18) | 현재 랜딩한 다이렉트 페이 심볼의 금액값
1.2|shuffledReelIdx | int Array(9 or 18) | 순서를 섞은 릴 인덱스
1.2|lockedReel | int Array(9 or 18) | 락이 걸려있는 릴 들의 배열(-1이면 lock이 안걸린것, 나머지 양수면 lock걸린 릴의 랜드값)
1.2|eachWin | int | 현재 표시할 EachWin 금액

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
    "result":[-1,1,-1],
    "isLinkMode":true,
    "randIds":[71,51,71,71,42,71,71,54,71],
    "initRands":[0,11,0,6,3,10,0,15,0],
    "winOnLock":[0,90,0,0,9000,0,0,225,0],
    "directPayOnLock":[-1,90,-1,-1,-1,-1,-1,225,-1],
    "shuffledReelIdx":[0,1,4,2,8,3,6,5,7],
    "lockedReel":[-1,11,-1,-1,3,-1,-1,15,-1],
    "eachWin":208352
}
```

> Error Response

```json
```


## Blue Link Game

### Response Parameters

Rev | Parameter | Default | Description
--------- | --------- | ------- | -----------
1|protocol | int(120) | SIG_SLOT_CUSTOM_ACTION
1|action | int(3) | 파시트에서 받아온 상수
1|code | int(200) | 서버 OK 리스폰스 넘버
1.2|shuffledRandArr | int Array(9) | 섞여진 릴들의 랜드값
1.2|shuffledRandsExceptLock | int Array(9) | -1이면 락이 걸린것, 나머지 숫자는 락이 걸린 랜드값
1.2|shuffledRandIds | int Array(9) | 랜드한 아이디 값들
1.2|currWinOnLock|int Array(9) | 각 심볼들에 걸린 금액
1.2|eachWin | int(0-max) | 현재 eachWin 값
1.2|viewTotalWin | int(0-max) | 현재보여줄 totalWin 값(리프레시의 경우 달라짐)
1.2|linkSpinTotalWin | int(0-max) | 링크스핀 전체의 획득 금액
1.2|initFreeSpinCount | int(0-max) | 링크스핀 진입 횟수
1.2|blueLinkSpinCount | int(0-max) | 남은 링크스핀 횟수
1.2|redSymbolCountArr | int(8-max) Array(배팅인덱스 수) | 레드 심볼 카운트를 배팅금액 당 저장한 어레이
1.2|blueSymbolCountArr | int(5-max) Array(배팅인덱스 수) | 블루 심볼 카운트를 배팅금액 당 저장한 어레이
1|jackpot | boolean | 잭팟 여부
1.2|phaseMultiple | int | 다음번 리프레시에서 전체 다이렉트 페이 심볼에 곱할 배수
1.2|isRefresh | boolean | 페이즈 변경 여부(리프레시)
1.2|shuffledReelIdx | int Array(9) | 순서를 섞은 릴 인덱스
1.2|lockedReel | int Array(9) | 락이 걸려있는 릴 들의 배열(-1이면 lock이 안걸린것, 나머지 양수면 lock걸린 릴의 랜드값)

### Response Parameters in DEBUG

Parameter | Default | Description
--------- | ------- | -----------
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
    "shuffledRandArr":[7,15,9,15,1,3,1,15,1],
    "shuffledRandsExceptLock":[-1,-1,-1,-1,-1,3,-1,-1,-1],
    "shuffledRandIds":[44,54,50,54,41,42,41,54,41],
    "currWinOnLock":[721,225,45,225,90000,9001,90000,225,90000],
    "eachWin":280442,
    "viewTotalWin":280442,
    "linkSpinTotalWin":280442,
    "initFreeSpinCount":5,
    "blueLinkSpinCount":2,
    "redSymbolCountArr":[8,8,9,8,8,8,8,8,8,8,8,8,8,8,8,8,8,8],
    "blueSymbolCountArr":[5,5,5,5,5,5,5,5,5,5,5,5,5,5,5,5,5,5],
    "jackpot":true,
    "phaseMultiple":1.2,
    "isRefresh":true,
    "shuffledReelIdx":[2,5,1,3,6,8,0,7,4],
    "lockedReel":[-1,-1,-1,-1,-1,-1,-1,-1,-1],
    "DEBUG_FOR_CLIENT_SYMBOL_INFO_ARR":[44,54,50,54,41,42,41,54,41]
}
```

> Error Response

```json
```

## Red Link Game

### Response Parameters

Rev | Parameter | Default | Description
--------- | --------- | ------- | -----------
1|protocol | int(120) | SIG_SLOT_CUSTOM_ACTION
1|action | int(2) | 파시트에서 받아온 상수
1|code | int(200) | 서버 OK 리스폰스 넘버
1.2|shuffledRandArr | int Array(18) | 섞여진 릴들의 랜드값
1.2|shuffledRandsExceptLock | int Array(18) | -1이면 락이 걸린것, 나머지 숫자는 락이 걸린 랜드값
1.2|shuffledRandIds | int Array(18) | 랜드한 아이디 값들
1.2|currWinOnLock|int Array(18) | 각 심볼들에 걸린 금액
1.2|eachWin | int(0-max) | 현재 eachWin 값
1.2|viewTotalWin | int(0-max) | 현재보여줄 totalWin 값(리프레시의 경우 달라짐)
1.2|linkSpinTotalWin | int(0-max) | 링크스핀 전체의 획득 금액
1.2|initFreeSpinCount | int(0-max) | 링크스핀 진입 횟수
1.2|redLinkSpinCount | int(0-max) | 남은 링크스핀 횟수
1.2|redSymbolCountArr | int(8-max) Array(배팅인덱스 수) | 레드 심볼 카운트를 배팅금액 당 저장한 어레이
1.2|blueSymbolCountArr | int(5-max) Array(배팅인덱스 수) | 블루 심볼 카운트를 배팅금액 당 저장한 어레이
1|jackpot | boolean | 잭팟 여부
1.2|phaseMultiple | int | 다음번 리프레시에서 전체 다이렉트 페이 심볼에 곱할 배수
1.2|isRefresh | boolean | 페이즈 변경 여부(리프레시)
1.2|shuffledReelIdx | int Array(18) | 순서를 섞은 릴 인덱스
1.2|lockedReel | int Array(18) | 락이 걸려있는 릴 들의 배열(-1이면 lock이 안걸린것, 나머지 양수면 lock걸린 릴의 랜드값)

### Response Parameters in DEBUG

Parameter | Default | Description
--------- | ------- | -----------
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
    "shuffledRandArr":[7,17,13,7,17,14,11,7,5,9,13,18,9,13,5,18,17,1],
    "shuffledRandsExceptLock":[-1,-1,-1,-1,-1,14,-1,-1,-1,-1,-1,-1,-1,-1,-1,-1,-1,-1],
    "shuffledRandIds":[44,53,52,44,53,23,51,44,43,50,52,99,50,52,43,99,53,41],
    "currWinOnLock":[720,180,135,720,180,0,90,720,1800,45,135,376785,45,135,1800,377865,180,90000],
    "eachWin":468000,
    "viewTotalWin":1022490,
    "linkSpinTotalWin":1874025,
    "initFreeSpinCount":8,
    "redLinkSpinCount":1,
    "redSymbolCountArr":[8,8,8,8,8,8,8,8,8,8,8,8,8,8,8,8,8,8],
    "blueSymbolCountArr":[5,5,5,5,5,5,5,5,5,5,5,5,5,5,5,5,5,5],
    "jackpot":false,
    "phaseMultiple":1.2,
    "isRefresh":false,
    "shuffledReelIdx":[11,14,6,2,8,9,1,7,4,13,17,15,0,3,10,12,5,16],
    "lockedReel":[7,17,13,7,17,-1,11,7,5,9,13,18,9,13,5,18,17,1],
    "DEBUG_FOR_CLIENT_SYMBOL_INFO_ARR":[44,53,52,44,53,23,51,44,43,50,52,99,50,52,43,99,53,41]
}
```

> Error Response

```json
```

## Claim Link Spin Total Win
Rev 1.2에서 추가  
링크스핀 끝날때 요청

### Response Parameters

Rev | Parameter | Default | Description
--------- | --------- | ------- | -----------
1.2|protocol | int(120) | SIG_SLOT_CUSTOM_ACTION
1.2|action | int(4) | 파시트에서 받아온 상수
1.2|code | int(200) | 서버 OK 리스폰스 넘버
1.2|linkSpinTotalWin | int(0-max) | 링크스핀 전체의 획득 금액
1.2|initFreeSpinCount | int(0-max) | 링크스핀 진입 횟수
1.2|redSymbolCount | int(0-max) | 현재(이번 스핀)까지 획득한 레드심볼 수
1.2|blueSymbolCount | int(0-max) | 현재(이번 스핀)까지 획득한 블루심볼 수
1.2|redSymbolCountArr | int(8-max) Array(배팅인덱스 수) | 레드 심볼 카운트를 배팅금액 당 저장한 어레이
1.2|blueSymbolCountArr | int(5-max) Array(배팅인덱스 수) | 블루 심볼 카운트를 배팅금액 당 저장한 어레이
1.2|betIndex | int(0-max) | Bet 금액 인덱스

> Request  

```javascript
// Define Pick Game Signal From parSheet
var SIG.CLAIM_LINK_SPIN_TOTAL_WIN = this.parSheet.actions.claimResultWin;

// Signal Handler on Client side
handle_signal: function( msg ) {
        switch( msg.protocol ) {
            case SIG.CLAIM_LINK_SPIN_TOTAL_WIN: {
                ...
            }
                break;
            ...
```

> Response

```json
{
    "protocol": 120,
    "action": 3,
    "code":200,
    "linkSpinTotalWin":1005165,
    "initFreeSpinCount":8,
    "blueSymbolCount":6,
    "redSymbolCount":8,
    "redSymbolCountArr":[8,8,8,8,8,8,8,8,8,8,8,8,8,8,8,8,8,8],
    "blueSymbolCountArr":[5,5,6,5,5,5,5,5,5,5,5,5,5,5,5,5,5,5],
    "betIndex":2
}
```

> Error Response

```json
```

## Claim Phase Change
Rev 1.2에서 추가  
페이즈 변할때 요청

### Response Parameters

Rev | Parameter | Default | Description
--------- | --------- | ------- | -----------
1.2|protocol | int(120) | SIG_SLOT_CUSTOM_ACTION
1.2|action | int(5) | 파시트에서 받아온 상수
1.2|code | int(200) | 서버 OK 리스폰스 넘버
1.2|betCash | int(0-max) | 배팅 금액
1.2|phaseChangeJackpotInfo | int(0-max) Array(4) | 페이즈 체인지할때의 잭팟 인포 배열
1.2|phaseMultiple | int | 리프레시에서 전체 다이렉트 페이 심볼에 곱할 배수

> Request  

```javascript
// Define Pick Game Signal From parSheet
var SIG.CLAIM_PHASE_CHANGE = this.parSheet.actions.claimPhaseChange;

// Signal Handler on Client side
handle_signal: function( msg ) {
        switch( msg.protocol ) {
            case SIG.CLAIM_PHASE_CHANGE: {
                ...
            }
                break;
            ...
```

> Response

```json
{
    "protocol": 120,
    "action": 4,
    "code":200,
    "betCash":90,
    "phaseChangeJackpotInfo":[720,1800,9000,90000],
    "phaseMultiple":1
}
```

> Error Response

```json
```

## Claim Phase Change
Rev 1.2에서 추가  
페이즈 변할때 인덱스를 담아서 요청

### Request Parameters

Rev | Parameter | Default | Description
--------- | --------- | ------- | -----------
1.2|protocol | int(120) | SIG_SLOT_CUSTOM_ACTION

### Response Parameters

Rev | Parameter | Default | Description
--------- | --------- | ------- | -----------
1.2|protocol | int(120) | SIG_SLOT_CUSTOM_ACTION
1.2|action | int(6) | 파시트에서 받아온 상수
1.2|code | int(200) | 서버 OK 리스폰스 넘버
1.2|jackpotType | string | `Minor`, `Minor`, `Minor`, `Minor` 중에 하나
1.2|betCash | int(0-max) | 배팅 금액
1.2|jackpotInfo | int(0-max) Array(4) | 새로운 잭팟 인포 배열
1.2|phaseMultiple | int | 리프레시에서 전체 다이렉트 페이 심볼에 곱할 배수

> Request  

```javascript
// Define Pick Game Signal From parSheet
var SIG.CLAIM_JACKPOT = this.parSheet.actions.claimJackpot;

// Signal Handler on Client side
handle_signal: function( msg ) {
        switch( msg.protocol ) {
            case SIG.CLAIM_JACKPOT: {
                ...
            }
                break;
            ...
```

> Response

```json
{
    "protocol": 120,
    "action": 6,
    "code":200,
    "jackpotType": "Minor",
    "betCash":90,
    "jackpotInfo":[720,1800,9000,90000],
    "phaseMultiple":1
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
1 | Pick Game | None
2 | blueLinkSpin | None
3 | redLinkSpin | None
4 | claimResultWin | grid(1d array) index 
5 | claimPhaseChange | None
6 | claimJackpot | index(int)
