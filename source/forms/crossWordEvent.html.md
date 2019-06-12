---
title: FILL IN THE BLANK Event Message Protocols

language_tabs: # must be one of https://git.io/vQNgJ
  - json

toc_footers:
  - <a href='https://alansynn.com'>Documented by Alan Synn</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# FILL IN THE BLANK Event 메시지 프로토콜 소개 문서

이하 호출 프로토콜에서 기본으로 필요한 `playerID`, `SIG_EVENT protocol`은 설명에서 제외

# Server Push messages

## Pick 획득시

Push 메시지로 `onPieceCrossWordEvent` 가 보내짐

> onPieceCrossWordEvent

```json
{
    "enableNextMission" : true,
    "showPieceBox"      : true,
    "eventStage"        : 0,
    "eventStep"         : 0,
    "eventRemainTime"   : 1817692380
}
```

## User level 10 달성시

Push 메시지로 `onUpdateCrossWordEvent` 가 보내짐

> onUpdateCrossWordEvent

```json
{ 
    "eventRemainTime"   : 1817692380
}
```

# In game

## CHECK

> 호출

```javascript
RockN.NET.request( 'connector.gameHandler.request', {
                    protocol: SIG.SIG_EVENT,
                    action: CW_EVENT_ACTION.CHECK,
                    playerID: RockN.Player.playerID
                }, func...
```

> 응답 예시

> 레벨 10이상, 이벤트기간 중, 미션완료전

```json
{
    "protocol": 340,
    "action": 0,
    "code": 200,
    "eventStage": 2,
    "eventStep": 2,
    "pickArr": [
        -1,"F","O","R","T",
        "U","N","E", -1, -1
    ],
    "pickResultArr": [
        1, -1, -1, 1, 1, 1, 1, 1, 1, 1
    ],
    "currMissionSentence": [
        -1, -1,"W","H","E","E","L", -1,"O","F", -1, -1,
        -1, -1,  1,  2,  3,  4,  5,  6,  7, -1, -1, -1,
        -1, -1,"P","O","W","E","R","P","O","I","N","T"
    ],
    "currAnswerSheet": [
        -1,"F","O","R","T","U","N","E", -1, -1
    ],
    "gauge": 25000000,
    "nextPickEnable": true,
    "nextPickBetGoal": 31500000,
    "prevPickBetGoal": 22950000,
    "pickProgress": 23.976608187134502,
    "currGauge": 2050000,
    "targetGauge": 8550000,
    "nextMissionEnable": true,
    "nextMissionBetGoal": 90000000,
    "leftPick": 1,
    "totalPick": 10,
    "eventRemainTime": 1817692380,
    "eventEnable": true,
    "completeReward": 1810000,
    "pickReward": 110000,
    "totalMissionReward": 12800000
}
```

> 이벤트 종료, 10미만  

```json
{
    "protocol": 340,
    "action": 0,
    "code": 200,
    "eventStage": 7,
    "nextPickEnable": false,
    "nextMissionEnable": false,
    "eventRemainTime": -1,
    "eventEnable": false,
}
```
array는 전부 1D

Parameter | Data | Description
--------- | ------- | -----------
pickArr | array | 후보 Array( -1은 꽝 )
pickResultArr | array | 플레이어가 고른 Array(직전 pick까지) -1이면 이미 고른것 1이면 남은것
currMissionSentence | array | 플레이어가 현재속한 스테이지의 문제(0이상이면 pickArr에서의 index)
currAnswerSheet | array | 플레이어가 현재 속한 스테이지의 정답(기획 변경 대비)
gauge | int | 플레이어의 현재 게이지
nextPickEnable | boolean | 플레이어가 다음 픽을 할 권한이 있는지(leftPick이 0이 아닐때)
nextPickBetGoal | int | 플레이어가 다음 픽을 하기위해서 필요한 베팅 금액
prevPickBetGoal | int | 플레이어가 이전 픽을 수행하기 위해서 필요했던 베팅 누적금액
pickProgress | int(0-100) | 다음 픽을 하기위한 게이지 충전 비율(퍼센트)
currGauge | int | 현재 게이지 충전 상태
targetGauge | int | 다음 픽을 하기위해서 필요한 게이지
nextMissionEnable | boolean | 다음 미션이 수행가능한지 여부
nextMissionBetGoal | int | 다음 미션을 수행하기위해서 필요한 베팅 금액
leftPick | int(0-10) | 남은 픽 갯수
totalPick | int(10) | 총 픽 가능 갯수(10개 후보가 있으므로 10)
eventRemainTime | int(-1 or ms) | 남은 이벤트 시간 (조건이 안될경우, 혹은 이벤트 종료시 -1)
eventEnable | boolean | 플레이어에게 이벤트가 가능한지 여부
completeReward | int | 현재 스테이지 리워드 금액
pickReward | int | 이번 픽 리워드 금액
totalMissionReward | int | 총 미션 클리어시 리워드 

## PICK

유저가 픽했을때 `pickIndex`를 PICK 코드(`2`)로 전달

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
pickIndex | int(0-10) | 플레이어가 고른 인덱스

> 호출

```javascript
RockN.NET.request( 'connector.gameHandler.request', {
                        protocol: SIG.SIG_EVENT,
                        action: CW_EVENT_ACTION.PICK,
                        pickIndex: pSender.index,
                        playerID: RockN.Player.playerID
                    }, func...
```

> 응답 예시

> 픽 성공

```json
{
    "protocol": 340,
    "action": 2,
    "code": 200,
    "reward": 8064,
    "eventStep": 3,
    "pickArr": [
        -1,"F","O","R","T",
        "U","N","E", -1, -1
    ],
    "pickArr": [
        1, -1, -1, 1, 1, 
        1, 1, 1, 1, 1
    ],
    "gauge": 25000000,
    "nextPickEnable": true,
    "nextPickBetGoal": 31500000,
    "nextMissionEnable": true,
    "eventRemainTime": 1815621344,
    "eventEnable": true
}
```

> 픽 실패 500에러

```json
{
    "protocol": 340,
    "action": 2,
    "code": 500,
    "reward": 0,
    "gauge": 25000000,
    "pickArr": [
        1, -1, -1, 1, 1, 
        1, 1, 1, 1, 1
    ],
    "nextPickEnable": false,
    "nextPickBetGoal": 31500000,
    "nextMissionEnable": true,
    "nextMissionBetGoal": 90000000,
    "eventRemainTime": 1815448829,
    "eventEnable": true
}
```

## COMPLETE MISSION

이벤트 완료시 

> 호출

```javascript
RockN.NET.request( 'connector.gameHandler.request', {
                    protocol: SIG.SIG_EVENT,
                    action: CW_EVENT_ACTION.COMPLETE_MISSION,
                    playerID: RockN.Player.playerID
                }, func
```

> 응답 예시
> 성공

```json
{
    "protocol": 340,
    "action": 3,
    "code": 200,
    "reward": 1810000,
    "gauge": 0,
    "nextPickEnable": false,
    "nextPickBetGoal": 31500000,
    "eventRemainTime": 1815119076,
    "eventEnable": true
}
```

> 실패 500에러

```json
{
    "protocol": 340,
    "action": 3,
    "code": 500,
    "reward": 0,
    "gauge": 0,
    "nextPickEnable": false,
    "nextPickBetGoal": 14400000,
    "eventRemainTime": 1815073107,
    "eventEnable": true
}
```

# Protocols

<aside class="notice">
프로토콜 문서
</aside>

Event 관련 부분 


Code | Meaning | Argument
---------- | ------- | -------
0 | CHECK | None
1 | CHECK_GAUGE(Not used) | None
2 | PICK | pickIndex
3 | COMPLETE MISSION | None