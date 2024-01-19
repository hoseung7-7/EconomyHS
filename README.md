# 이 스크립트는 배포를 목적으로 만들어졌습니다.
# 2차 배포 시 스크립트 배포 중단하겠습니다.
# EconomyHS ver 1.0 dev.
# Copyright 2024. hoseung7_7 all rights reserved.
# EconomyHS API를 활용한 창작은 가능합니다.


on load:
	wait 2 seconds
	broadcast "                                  "
	broadcast " &6EconomyHS 스크립트 제작자 &7: &fhoseung7_7 "
	broadcast " &e해당 스크립트는 &b배포용 &e스크립트 입니다. "
	broadcast " Copyright 2024. hoseung_7 all rights reserved.       "                   
	broadcast "													"
	set {firstmoney} to 100
	stop
	
on first join:
	set {money.%player%} to {firstmoney}
	message "기본적으로 지급되는 돈인 %{firstmoney}%이 지급되었습니다. 즐거운 시간되세요~!" to player
	stop

#deop	
command /money:
	trigger:
		message "현재 %player%님이 보유하신 자금은 %{money.%player%}%원 입니다" to player
		stop

command /sendmoney [<player>] [<integer>]:
	trigger:
		if {money.%player%} >= arg-2:
			add arg-2 to {money.%arg-1%}
			subtract arg-2 from {money.%player%}
			send "%arg-1%님에게 %arg-2%를 송금하였습니다. 남은 잔액: %{money.%player%}%원"
		else:
			send "보내려는 금액이 가지고 있는 금액보다 큽니다!"
			stop
			
command /seemoney [<player>]:
	trigger:
		if arg-1 is set:
			send "%arg-1%님의 자금은 %{money.%arg-1%}%원입니다."
			stop
#op 
command /givemoney [<player>] [<integer>]:
	trigger:
		if player is op:
			if arg-2 is set:
				if arg-1 is set:
					add arg-2 to {money.%arg-1%}
					send "관리자가 %arg-2%원을 %arg-1%님에게 주었습니다 남은 자금: %{money.%player%}%원" 
		else:
			send "당신은 관리자가 아닙니다"
			stop
			
command /takemoney [<player>] [<integer>]:
	trigger:
		if player is op:
			if arg-2 is set:
				if arg-1 is set:
					subtract arg-2 from {money.%arg-1%} 
					send "%arg-1%의 남은 남은 잔액: %{money.%arg-1%}%원"
		else:
			send "당신은 관리자가 아닙니다"
			stop
			
#op gui
command /opgui:
	trigger:
		open chest inventory with 1 row named "&cEconomy Control" to player
		stop
