--[[
  Polsec / Rivals 中文自動層 v3
  - 自動載入原腳本 + 中文
  - 不碰遊戲 UI、不用 CoreGui
]]

local Players = game:GetService("Players")

local function waitReady()
	local lp = Players.LocalPlayer or Players.PlayerAdded:Wait()
	if not lp.Character then lp.CharacterAdded:Wait() end
	task.wait(0.8)
end
pcall(waitReady)

local LOADER = "https://api.polsec.net/loader/f1741ef3a2610ac7/78c2720d864f3b30"
task.spawn(function()
	pcall(function()
		local src = game:HttpGet(LOADER)
		local fn = loadstring(src)
		if fn then fn() end
	end)
end)

local MAP = {
	-- 分頁 / 子分頁
	["Weapon Aim"] = "武器瞄準",
	["Viewmodel"] = "第一人稱",
	["Character"] = "角色",
	["Visuals"] = "視覺",
	["World"] = "世界",
	["Main"] = "主頁",
	["Esp"] = "透視",
	["ESP"] = "透視",
	["Auto Loadout"] = "自動裝備",
	["Auto Queue"] = "自動排隊",
	["Auto Ban Weapon"] = "自動禁用武器",
	["Ban Weapon"] = "禁用武器",
	["Unlocks"] = "解鎖",
	["Rank Charm"] = "段位掛飾",
	["Mod Detector"] = "外掛偵測",
	["Hit Sound"] = "擊中音效",
	["Device Spoof"] = "裝置偽裝",
	["Sound Spammer"] = "音效洗版",
	["Stretch Resol"] = "拉伸解析度",
	["Stretch Resolution"] = "拉伸解析度",
	["Miscellaneous"] = "雜項",
	["Spoof"] = "偽裝",
	["Spoof End Streak"] = "偽裝連勝結束",
	["Gaming Chair"] = "電競椅",
	["Chair Effects"] = "椅子特效",
	["Aura"] = "光環",
	["Slide Boost"] = "滑鏟加速",
	["Third Person"] = "第三人稱",
	["Animation Player"] = "動畫播放器",
	["Target Hud"] = "目標 HUD",
	["Soul Particles"] = "靈魂粒子",
	["Hit Overlay"] = "擊中覆蓋",
	["Eliminated Spoofer"] = "擊殺文字偽裝",
	["Bullet Tracers"] = "子彈軌跡",
	["Shoot Sound"] = "射擊音效",
	["Damage Numbers"] = "傷害數字",
	["Weapon Status"] = "武器狀態",
	["Game Healthbar"] = "遊戲血條",
	["Crosshair Effects"] = "準星特效",
	["Crosshair Image"] = "準星圖片",
	["Crosshair"] = "準星",
	["Ingame Hit Effects"] = "遊戲內擊中特效",
	["Texture Pack"] = "材質包",
	["Performance Fflags"] = "效能旗標",
	["Modulation"] = "調色",
	["Weather"] = "天氣",
	["Removals"] = "移除",
	["Skybox"] = "天空盒",
	["Atmosphere"] = "大氣",
	["Color Shift"] = "色偏",
	["Interface"] = "介面",
	["Startup"] = "啟動",
	["Configurations"] = "設定檔",
	["Community Configs"] = "社群設定檔",
	["Theme"] = "主題",
	["Animations"] = "動畫",
	["Ffa Settings"] = "FFA 設定",
	["Hit Notify"] = "擊中通知",
	["Hit Notify Style"] = "擊中通知樣式",
	["Gun Material"] = "槍材質",
	["Gun Highlight"] = "槍高亮",
	["Wireframe"] = "線框",
	["Gun Size"] = "槍尺寸",
	["Disable Anims"] = "關閉動畫",
	["Custom Arms"] = "自訂手臂",
	["Arm Chams"] = "手臂材質",
	["Arms Highlight"] = "手臂高亮",
	["Arms Wireframe"] = "手臂線框",
	["Gun Glow"] = "槍發光",
	["Arm Glow"] = "手臂發光",
	["Offsets"] = "偏移",
	["Silent Aim"] = "靜默瞄準",
	["Aimbot"] = "自瞄",
	["Ragebot"] = "狂暴自瞄",
	["Translocate"] = "瞬移",
	["Triggerbot"] = "自動開槍",
	["Anti Aim"] = "反自瞄",

	-- 通用
	["enable"] = "啟用",
	["Enable"] = "啟用",
	["enabled"] = "啟用",
	["Enabled"] = "啟用",
	["notify"] = "通知",
	["Notify"] = "通知",
	["type"] = "類型",
	["Type"] = "類型",
	["mode"] = "模式",
	["Mode"] = "模式",
	["rank"] = "段位",
	["Rank"] = "段位",
	["name"] = "名稱",
	["Name"] = "名稱",
	["username"] = "使用者名稱",
	["Username"] = "使用者名稱",
	["display name"] = "顯示名稱",
	["Display Name"] = "顯示名稱",
	["status"] = "狀態",
	["Status"] = "狀態",
	["level"] = "等級",
	["Level"] = "等級",
	["avatar"] = "頭像",
	["Avatar"] = "頭像",
	["solid"] = "純色",
	["Solid"] = "純色",
	["intensity"] = "強度",
	["Intensity"] = "強度",
	["radius"] = "半徑",
	["Radius"] = "半徑",
	["None"] = "無",
	["Head"] = "頭部",
	["Default"] = "預設",

	-- Mod Detector
	["moderator actions"] = "管理員動作",
	["mod friend actions"] = "管理員好友動作",

	-- Device Spoof / Sound / Ban
	["custom icon color"] = "自訂圖示顏色",
	["MouseKeyboard"] = "滑鼠鍵盤",
	["sound type"] = "音效類型",
	["Double Jump"] = "二段跳",
	["weapons to ban"] = "要禁用的武器",
	["season charm"] = "賽季掛飾",
	["optional, e.g. 1"] = "選填，例如 1",
	["optional, e.g.1"] = "選填，例如 1",

	-- Miscellaneous
	["auto destroy tripmine"] = "自動摧毀地雷",
	["anti smoke"] = "反煙霧",
	["anti flash"] = "反閃光",
	["no scope overlay"] = "無開鏡遮罩",
	["no projectile visuals"] = "無投射物視覺",

	-- Spoof 欄位
	["weapon keys"] = "武器鑰匙",
	["event currency"] = "活動貨幣",
	["casual wins"] = "休閒勝場",
	["ranked wins"] = "排位勝場",
	["casual win percent"] = "休閒勝率",
	["ranked win percent"] = "排位勝率",
	["ranked elo"] = "排位 Elo",
	["leaderboard rank"] = "排行榜名次",
	["favorite map"] = "最愛地圖",
	["influencer"] = "網紅",
	["roblox employee"] = "Roblox 員工",
	["nosniy games team"] = "Nosniy 團隊",
	["ping value"] = "延遲數值",
	["ping spoof"] = "延遲偽裝",
	["win streak"] = "連勝",
	["status type"] = "狀態類型",
	["user name or display name"] = "使用者名稱或顯示名稱",
	["send end streak"] = "發送結束連勝",

	-- Unlocks
	["unlock all"] = "解鎖全部",
	["auto load unlock all"] = "自動載入解鎖全部",

	-- 第一人稱
	["no hands"] = "無手",
	["disable clothes"] = "關閉衣服",
	["color mode"] = "顏色模式",
	["color 模式"] = "顏色模式",
	["gradient directions"] = "漸層方向",
	["gun highlight above"] = "槍高亮置頂",
	["arm chams"] = "手臂材質",
	["arm no texture"] = "手臂無貼圖",
	["arm above"] = "手臂置頂",
	["valorant arms"] = "Valorant 手臂",
	["cycle speed"] = "循環速度",
	["Neon"] = "霓虹",
	["SmoothPlastic"] = "光滑塑膠",

	-- 瞄準
	["closest part"] = "最近部位",
	["Closest Part"] = "最近部位",
	["hit part"] = "命中部位",
	["Hit Part"] = "命中部位",
	["hit chance"] = "命中機率",
	["Hit Chance"] = "命中機率",
	["show fov"] = "顯示 FOV",
	["Show FOV"] = "顯示 FOV",
	["follow gunpoint"] = "跟隨槍口",
	["Follow Gunpoint"] = "跟隨槍口",
	["follow target"] = "跟隨目標",
	["Follow Target"] = "跟隨目標",
	["show fill"] = "顯示填充",
	["Show Fill"] = "顯示填充",
	["lerp"] = "平滑",
	["Lerp"] = "平滑",
	["fill transparency"] = "填充透明度",
	["Fill Transparency"] = "填充透明度",
	["fov transparency"] = "FOV 透明度",
	["FOV Transparency"] = "FOV 透明度",
	["thickness"] = "粗細",
	["Thickness"] = "粗細",
	["rotation speed"] = "旋轉速度",
	["Rotation Speed"] = "旋轉速度",
	["team check"] = "隊友檢測",
	["Team Check"] = "隊友檢測",
	["disable on scope"] = "開鏡時關閉",
	["Disable On Scope"] = "開鏡時關閉",
	["whitelist part"] = "白名單部位",
	["Whitelist Part"] = "白名單部位",
	["reaction time"] = "反應時間",
	["Reaction Time"] = "反應時間",
	["shoot delay"] = "射擊延遲",
	["Shoot Delay"] = "射擊延遲",
	["sniper scoped"] = "狙擊開鏡",
	["Sniper Scoped"] = "狙擊開鏡",
	["use weapon settings"] = "使用武器設定",
	["Use Weapon Settings"] = "使用武器設定",
	["fov radius"] = "FOV 半徑",
	["FOV Radius"] = "FOV 半徑",
	["checks"] = "檢查",
	["Checks"] = "檢查",
	["anti knife"] = "反小刀",
	["void spam"] = "虛空洗版",
	["void hide amount"] = "虛空隱藏時間",
	["attack seconds"] = "攻擊秒數",
	["swap weapon on empty"] = "空彈時切換武器",
	["priority weapon"] = "優先武器",
	["safe method"] = "安全方法",
	["random pos"] = "隨機位置",
	["underground depth"] = "地下深度",
	["attack mode"] = "攻擊模式",
	["gun"] = "槍",
	["swap when"] = "何時切換",
	["ammo reserve"] = "備用彈藥",
	["auto crouch"] = "自動蹲下",
	["smart target prioritization (ffa)"] = "智慧目標優先（FFA）",
	["ffa target priorities"] = "FFA 目標優先",
	["lowest health"] = "最低血量",
	["anti translocate"] = "反瞬移",
	["offset"] = "偏移",

	-- 武器增強
	["Weapons"] = "武器",
	["rapid fire"] = "連射",
	["Rapid Fire"] = "連射",
	["remove melee cooldown"] = "移除近戰冷卻",
	["Remove Melee Cooldown"] = "移除近戰冷卻",
	["remove warhorn cooldown"] = "移除號角冷卻",
	["Remove Warhorn Cooldown"] = "移除號角冷卻",
	["no spread"] = "無擴散",
	["No Spread"] = "無擴散",
	["faster reload"] = "加快換彈",
	["Faster Reload"] = "加快換彈",
	["no muzzle"] = "無槍口焰",
	["No Muzzle"] = "無槍口焰",
	["no recoil"] = "無後座",
	["No Recoil"] = "無後座",
	["automatic weapon"] = "全自動",
	["Automatic Weapon"] = "全自動",
	["throwable options"] = "投擲物選項",
	["Throwable Options"] = "投擲物選項",
	["always backstab"] = "永遠背刺",
	["Always Backstab"] = "永遠背刺",
	["more health (needs riot shield)"] = "更多血量（需防暴盾）",
	["More Health (needs riot shield)"] = "更多血量（需防暴盾）",
	["pitch"] = "俯仰",
	["yaw"] = "偏航",
	["jitter"] = "抖動",
	["down"] = "向下",

	-- 武器名
	["Assault Rifle"] = "突擊步槍",
	["Burst Rifle"] = "連發步槍",
	["Energy Rifle"] = "能量步槍",
	["Energy Pistols"] = "能量手槍",
	["Flare Gun"] = "信號槍",
	["Freeze Ray"] = "冷凍射線",
	["Glass Cannon"] = "玻璃大砲",
	["Grenade Launcher"] = "榴彈發射器",
	["Gunblade"] = "槍刃",
	["Exogun"] = "Exogun",
	["Daggers"] = "匕首",
	["Distortion"] = "扭曲",
	["Crossbow"] = "弩",
	["Bow"] = "弓",
	["Handgun"] = "手槍",
	["Fists"] = "拳頭",
	["Grenade"] = "手榴彈",
	["Sniper"] = "狙擊槍",
	["Shotgun"] = "霰彈槍",
	["RPG"] = "火箭筒",
	["Minigun"] = "加特林",
	["Flamethrower"] = "火焰噴射器",
	["Paintball Gun"] = "漆彈槍",
	["Scepter"] = "權杖",
	["Permafrost"] = "永凍",
	["Warper"] = "傳送槍",
	["Slingshot"] = "彈弓",
	["Revolver"] = "左輪手槍",
	["Shorty"] = "短管霰彈",
	["Spray"] = "噴漆槍",
	["Uzi"] = "烏茲衝鋒槍",
	["Trowel"] = "泥刀",
	["Battle Axe"] = "戰斧",
	["Chainsaw"] = "電鋸",
	["Katana"] = "武士刀",
	["Knife"] = "小刀",
	["Scythe"] = "鐮刀",
	["Riot Shield"] = "防暴盾",
	["Glast Shard"] = "玻璃碎片",
	["Medkit"] = "醫療包",
	["Subspace Tripmine"] = "子空間地雷",
	["Warpstone"] = "傳送石",
	["Flashbang"] = "閃光彈",
	["Jump Pad"] = "彈跳墊",
	["Molotov"] = "燃燒瓶",
	["Spear"] = "長矛",
	["Maul"] = "巨錘",
	["Grappler"] = "抓鉤",
	["War Horn"] = "戰爭號角",
	["Satchel"] = "沙袋炸彈",
	["Smoke Grenade"] = "煙霧彈",
	["primary"] = "主武器",
	["secondary"] = "副武器",
	["melee"] = "近戰",
	["utility"] = "功能道具",
	["Primary"] = "主武器",
	["Secondary"] = "副武器",
	["Melee"] = "近戰",
	["Utility"] = "功能道具",

	-- ESP / Visuals
	["master switch"] = "總開關",
	["Master Switch"] = "總開關",
	["box outline"] = "方框外框",
	["Box Outline"] = "方框外框",
	["box mode"] = "方框模式",
	["Box Mode"] = "方框模式",
	["box animated"] = "方框動畫",
	["box anim speed"] = "方框動畫速度",
	["box transparency"] = "方框透明度",
	["corner length"] = "邊角長度",
	["corner thickness"] = "邊角粗細",
	["box fill"] = "方框填充",
	["fill animated"] = "填充動畫",
	["fill anim speed"] = "填充動畫速度",
	["health bar width"] = "血條寬度",
	["health bar offset"] = "血條偏移",
	["health bar"] = "血條",
	["Health Bar"] = "血條",
	["dynamic health color"] = "動態血量顏色",
	["health text"] = "血量文字",
	["name animated"] = "名稱動畫",
	["name anim speed"] = "名稱動畫速度",
	["distance animated"] = "距離動畫",
	["distance anim speed"] = "距離動畫速度",
	["weapon animated"] = "武器動畫",
	["weapon anim speed"] = "武器動畫速度",
	["weapon icon scale"] = "武器圖示縮放",
	["weapon icon"] = "武器圖示",
	["ammo animated"] = "彈藥動畫",
	["ammo anim speed"] = "彈藥動畫速度",
	["show reloading"] = "顯示換彈中",
	["typewriter text"] = "打字機文字",
	["text size"] = "文字大小",
	["max distance"] = "最大距離",
	["infinite max distance"] = "無限最大距離",
	["show targets"] = "顯示目標來源",
	["ui scale"] = "UI 縮放",
	["item scale"] = "項目縮放",
	["duration"] = "持續時間",
	["distance"] = "距離",
	["weapon"] = "武器",
	["ammo"] = "彈藥",
	["font"] = "字體",
	["Full"] = "完整",
	["Corner"] = "邊角",

	-- 角色
	["noclip"] = "無碰撞",
	["fly"] = "飛行",
	["fly speed"] = "飛行速度",
	["spinbot"] = "旋轉機器人",
	["spinbot speed"] = "旋轉速度",
	["walkspeed multiplier"] = "走路速度倍率",
	["walkspeed"] = "走路速度",
	["jumppower multiplier"] = "跳躍力倍率",
	["jumppower"] = "跳躍力",
	["infinite jump"] = "無限跳躍",
	["auto slide"] = "自動滑鏟",
	["unlock mouse"] = "解鎖滑鼠",
	["animation"] = "動畫",
	["speed"] = "速度",
	["material"] = "材質",
	["transparency"] = "透明度",
	["size"] = "大小",
	["sitting animation"] = "坐下動畫",
	["flight fan"] = "飛行風扇",
	["fan speed"] = "風扇速度",
	["wheel trails"] = "輪子軌跡",
	["override color"] = "覆蓋顏色",
	["auras"] = "光環",
	["starlight"] = "星光",
	["trail lifetime"] = "軌跡存活時間",
	["outline above"] = "外框置頂",
	["height offset"] = "高度偏移",

	-- 其他
	["finish load"] = "完成載入",
	["queue mode"] = "排隊模式",
	["instant auto queue"] = "即時自動排隊",
	["grab drops"] = "撿取掉落物",
	["auto respawn"] = "自動重生",
	["preview notification"] = "預覽通知",
	["text color"] = "文字顏色",
	["maximum visible"] = "最大可見數",
	["spacing"] = "間距",
	["stack direction"] = "堆疊方向",
	["background"] = "背景",
	["background color"] = "背景顏色",
	["background transparency"] = "背景透明度",
	["text outline"] = "文字外框",
	["custom target color"] = "自訂目標顏色",
	["target color"] = "目標顏色",
	["custom damage color"] = "自訂傷害顏色",
	["damage color"] = "傷害顏色",
	["gradient"] = "漸層",
	["gradient start"] = "漸層起點",
	["gradient end"] = "漸層終點",
	["fade"] = "淡出",
	["remove ingame hit sound"] = "移除遊戲內擊中音效",
	["import sound"] = "匯入音效",
	["refresh imported sounds"] = "重新整理已匯入音效",
	["preview sound"] = "預覽音效",
	["volume"] = "音量",

	-- World / 設定
	["ambient"] = "環境光",
	["brightness"] = "亮度",
	["clock time"] = "時鐘時間",
	["environment diffuse scale"] = "環境漫射",
	["environment specular scale"] = "環境高光",
	["exposure compensation"] = "曝光補償",
	["fog color"] = "霧顏色",
	["fog end"] = "霧終點",
	["fog start"] = "霧起點",
	["global shadows"] = "全域陰影",
	["outdoor ambient"] = "室外環境光",
	["shadow softness"] = "陰影柔和度",
	["technology"] = "渲染技術",
	["selected"] = "已選",
	["color shift top"] = "色偏上",
	["color shift bottom"] = "色偏下",
	["custom color"] = "自訂顏色",
	["types"] = "類型",
	["rate"] = "速率",
	["visibility"] = "可見度",
	["particle size"] = "粒子大小",
	["particle speed"] = "粒子速度",
	["no textures"] = "無貼圖",
	["skybox"] = "天空盒",
	["density"] = "密度",
	["glare"] = "眩光",
	["haze"] = "霾",
	["refresh skyboxes"] = "重新整理天空盒",
	["export client settings"] = "匯出客戶端設定",
	["unload fflags"] = "卸載旗標",
	["pack"] = "材質包",
	["Watermark details"] = "浮水印內容",
	["Watermark"] = "浮水印",
	["Keybind list"] = "快捷鍵列表",
	["Menu buttons"] = "選單按鈕",
	["Menu key"] = "選單按鍵",
	["Unload"] = "卸載",
	["Auto load"] = "自動載入",
	["Silent load"] = "靜默載入",
	["Config name"] = "設定檔名稱",
	["Create config"] = "建立設定檔",
	["Save selected"] = "儲存選中",
	["Load selected"] = "載入選中",
	["Delete selected"] = "刪除選中",
	["Refresh configs"] = "重新整理設定檔",
	["Set auto load"] = "設為自動載入",
	["Clear auto load"] = "清除自動載入",
	["Copy current config"] = "複製目前設定",
	["Paste config"] = "貼上設定",
	["Restore default background"] = "還原預設背景",
	["Saved config"] = "已存設定檔",
	["Accent"] = "強調色",
	["Background"] = "背景",
	["Inline"] = "內框",
	["Content"] = "內容",
	["Inactive Text"] = "未啟用文字",
	["Hovered Element"] = "滑過元素",
	["Outline 1"] = "外框 1",
	["Outline 2"] = "外框 2",
	["Outline 3"] = "外框 3",
	["Outline 4"] = "外框 4",
	["Auto Load"] = "自動載入",
	["auto load"] = "自動載入",
	["Set Auto Load"] = "設為自動載入",
	["Clear Auto Load"] = "清除自動載入",
	["Silent Load"] = "靜默載入",

	-- Visuals 補漏
	["image size"] = "圖片大小",
	["image transparency"] = "圖片透明度",
	["local images"] = "本機圖片",
	["Place images in Elisium/V2/Assets/crosshair-images."] = "請將圖片放在 Elisium/V2/Assets/crosshair-images。",
	["refresh image list"] = "重新整理圖片列表",
	["texture"] = "材質",
	["lightning"] = "閃電",
	["position"] = "位置",
	["lifetime"] = "存活時間",
	["width start"] = "起始寬度",
	["width end"] = "結束寬度",
	["sound"] = "音效",
	["hitmarker"] = "擊中音",
	["disable ingame damage numbers"] = "關閉遊戲內傷害數字",
	["strength"] = "強度",
	["show eliminated text"] = "顯示擊殺文字",
	["name placement"] = "名稱位置",
	["after text"] = "後方文字",
	["custom name color"] = "自訂名稱顏色",
	["custom screen position"] = "自訂螢幕位置",
	["screen x"] = "螢幕 X",
	["screen y"] = "螢幕 Y",
	["custom text size"] = "自訂文字大小",
	["text and name gradient"] = "文字與名稱漸層",
	["gradient angle"] = "漸層角度",
	["static"] = "靜態",
	["entrance animation"] = "進場動畫",
	["animation duration"] = "動畫時長",
	["rotating"] = "旋轉",
	["pulsing spread"] = "脈衝擴散",
	["minimum spread"] = "最小擴散",
	["maximum spread"] = "最大擴散",
	["spread speed"] = "擴散速度",
	["follow mode"] = "跟隨模式",
	["color animation"] = "顏色動畫",
	["shimmer"] = "微光",
	["shimmer fade color"] = "微光淡出顏色",
	["ping pong background"] = "來回背景",
	["ping pong main color"] = "來回主色",
	["ping pong angle"] = "來回角度",
	["gap"] = "間距",
	["outline thickness"] = "外框粗細",
	["outline"] = "外框",
	["outline color"] = "外框顏色",
	["top line"] = "上線",
	["bottom line"] = "下線",
	["left line"] = "左線",
	["right line"] = "右線",
	["override weapon status"] = "覆蓋武器狀態",
	["hide healthbar"] = "隱藏血條",
	["custom size"] = "自訂大小",
	["width"] = "寬度",
	["height"] = "高度",
	["replace health number"] = "替換血量數字",
	["hide heart icon"] = "隱藏愛心圖示",
	["custom position"] = "自訂位置",
	["horizontal position"] = "水平位置",
	["vertical position"] = "垂直位置",
	["damage number colors"] = "傷害數字顏色",
	["hit marker colors"] = "擊中標記顏色",
	["style"] = "樣式",
	["Lines"] = "線條",
	["rotation"] = "旋轉",
	["length"] = "長度",
	["follow target"] = "跟隨目標",
	["color"] = "顏色",

	["enabled"] = "啟用",
	["material"] = "材質",
	["color mode"] = "顏色模式",
	["gradient directions"] = "漸層方向",
	["cycle speed"] = "循環速度",
	["fill transparency"] = "填充透明度",
	["outline transparency"] = "外框透明度",
	["gun highlight above"] = "槍高亮置頂",
	["Gun Material"] = "槍材質",
	["Gun Highlight"] = "槍高亮",
	["Removals"] = "移除",
	["Custom Arms"] = "自訂手臂",
	["Arm Chams"] = "手臂材質",
	["Arms Highlight"] = "手臂高亮",
	["Arms Wireframe"] = "手臂線框",
	["Gun Glow"] = "槍發光",
	["Arm Glow"] = "手臂發光",
	["Wireframe"] = "線框",
	["length"] = "長度",
	["transparency"] = "透明度",
	["intensity"] = "強度",
	["radius"] = "半徑",
	["solid"] = "純色",
	["Neon"] = "霓虹",
}

-- 不翻譯遊戲本身文字
local SKIP = {
	["前往決鬥"] = true, ["擊殺次數"] = true, ["遊戲時間"] = true,
	["背包"] = true, ["武器"] = true, ["任務"] = true, ["商店"] = true,
	["通行證"] = true, ["恢復"] = true, ["活動"] = true, ["狙擊手"] = true,
	["Back"] = true, ["Keyless"] = true, ["Keyless | Keyless"] = true,
	["Nosniy"] = true, ["Elisium"] = true, ["Arena"] = true, ["Prime"] = true,
	["Low"] = true, ["Season 3 (Fame)"] = true,
}

local keys = {}
for k in pairs(MAP) do table.insert(keys, k) end
table.sort(keys, function(a, b) return #a > #b end)

local function translateText(s)
	if typeof(s) ~= "string" or s == "" or #s > 120 then return s end
	if SKIP[s] then return s end
	if not s:match("[A-Za-z]") then return s end
	if MAP[s] then return MAP[s] end
	-- 小寫比對（選單有時大小寫不一）
	local lower = string.lower(s)
	for eng, zh in pairs(MAP) do
		if string.lower(eng) == lower then return zh end
	end
	local out = s
	for _, eng in ipairs(keys) do
		if out:find(eng, 1, true) then
			out = out:gsub(eng, MAP[eng])
		end
	end
	return out
end

local done = setmetatable({}, { __mode = "k" })

local function tryOne(obj)
	if done[obj] then return end
	local isText = false
	pcall(function()
		isText = obj:IsA("TextLabel") or obj:IsA("TextButton") or obj:IsA("TextBox")
	end)
	if not isText then return end
	pcall(function()
		local t = obj.Text
		if SKIP[t] or t == "" then done[obj] = true return end
		local nt = translateText(t)
		if nt ~= t then obj.Text = nt end
		if obj:IsA("TextBox") and obj.PlaceholderText and obj.PlaceholderText ~= "" then
			local p = obj.PlaceholderText
			local np = translateText(p)
			if np ~= p then obj.PlaceholderText = np end
		end
		done[obj] = true
	end)
end

local function getRoot()
	local r
	pcall(function()
		if typeof(gethui) == "function" then r = gethui() end
	end)
	if r then return r end
	local lp = Players.LocalPlayer
	return lp and lp:FindFirstChild("PlayerGui")
end

-- 掃描 gethui 下所有 ScreenGui（不只名稱符合的），靠 SKIP 避開遊戲文字
local function scanAll()
	local root = getRoot()
	if not root then return end
	pcall(function()
		for _, child in ipairs(root:GetChildren()) do
			local ok = false
			pcall(function() ok = child:IsA("ScreenGui") or child:IsA("Folder") or child:IsA("Frame") end)
			if ok then
				for _, obj in ipairs(child:GetDescendants()) do
					tryOne(obj)
				end
			end
		end
	end)
end

task.spawn(function()
	task.wait(2.5)

	-- 先掃幾次把現有選單翻完
	for _ = 1, 8 do
		scanAll()
		task.wait(0.5)
	end
	print("[河馬] 中文層就緒（輕量持續掃描）")

	local root = getRoot()
	if root then
		-- 新節點出現就翻（幾乎不卡）
		pcall(function()
			root.DescendantAdded:Connect(function(obj)
				task.defer(tryOne, obj)
			end)
		end)
	end

	-- 輕量補掃：每 4 秒一次，且每批只處理有限數量，避免卡
	while true do
		task.wait(4)
		local root2 = getRoot()
		if not root2 then continue end
		local batch = 0
		pcall(function()
			for _, child in ipairs(root2:GetChildren()) do
				local ok = false
				pcall(function()
					ok = child:IsA("ScreenGui") or child:IsA("Folder") or child:IsA("Frame")
				end)
				if not ok then continue end
				for _, obj in ipairs(child:GetDescendants()) do
					if not done[obj] then
						tryOne(obj)
						batch = batch + 1
						if batch % 80 == 0 then
							task.wait() -- 讓出一幀，不卡
						end
					end
				end
			end
		end)
	end
end)
