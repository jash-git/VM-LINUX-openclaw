在VM內LINUX安裝openclaw完整步驟紀錄 [VM+LINUX+openclaw]

資料來源: https://www.youtube.com/watch?v=rggcjvP2i0Q
https://www.dhzyw.com/archives/7891.html
https://chatgpt.com/share/69be975a-ff0c-8008-908c-7d7e5bb396c9
https://www.youtube.com/watch?v=A4PLqwDligE
https://www.youtube.com/watch?v=F9f02BeA_Ms
https://www.youtube.com/watch?v=jn7FzlTCyDw
https://www.dhzyw.com/archives/7940.html

基礎環境準備
	00.VM網路 NAT和橋接的差別: 橋接（Bridged）模式讓虛擬機在區域網路中獲得獨立 IP，與宿主機地位相同，適合需被外部訪問的伺服器場景；NAT 模式則是虛擬機共享宿主機 IP，通過宿主機進行網路轉換，隱藏在內部，適合需要上網但無需外部訪問的開發測試環境。

	
	01.更新軟體的最新資訊及列表
	sudo apt-get update


	02.更新目前已安裝的軟體到最新版本
	sudo apt-get upgrade


	03.安裝OpenSSH
	sudo apt install -y openssh-server


	04.安裝CURL
	sudo apt install -y curl


	05.安裝node.js
	sudo apt-get install nodejs
	sudo apt install npm
	nodejs -v
	npm -v


	06.安裝 nvm
	curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
	重開機

	07.安裝nodejs 22 [AI: Node.js v18.19.1 found, upgrading to v22+ 在LINUX 我要如何處理]
	nvm install 22
	nvm alias default 22
	重開機
	nodejs -v


	08.安裝建置和編譯軟體所需的基本工具和函式庫
	sudo apt install build-essential


====================
一鍵安裝OpenClaw
	curl -fsSL https://openclaw.ai/install.sh | bash	
		openclaw onboard --install-daemon [隨時可以重新進入設定介面指令 /Ctrl+C 可以中斷設置] 27:10


====================
OpenClaw和本地Ollama串接
	01.圖01~02是第一次設定WSS資訊 28:24
	
	
	02.圖03~09是第二次設定綁定Ollama資訊 30:21
		http://192.168.0.178:11434/
	
	03.讀取VM IP: 192.168.0.102 30:39  30:47
		ifconfig
		grep '"token"' ~/.openclaw/openclaw.json  提取登入時要的token
			c1f8384f514b0e5c44745d31e0e17282e31110f5c7948aad
			
	
	04.WINDOWS轉發WSS
		PowerShell: ssh -L 18789:127.0.0.1:18789 vblinux@192.168.0.102
			vblinux:虛擬機器名稱
			192.168.0.102:虛擬機器IP
			
			
	05.WINDOWS/Linux 在瀏覽器使用龍蝦
		http://localhost:18789/
			c1f8384f514b0e5c44745d31e0e17282e31110f5c7948aad
			密碼:asd700502


===========
龍蝦命令:
	啟用~     openclaw gateway start
	停止~     openclaw gateway stop
	重新配置~ openclaw config  [openclaw gateway]
	重開~     openclaw gateway restart
	開啟檔案權限:
		openclaw config set tools.profile full
		openclaw gateway restart
	安裝Skills:
		https://www.youtube.com/watch?v=F9f02BeA_Ms