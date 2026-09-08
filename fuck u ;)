-- // HATE v18 FINAL (PART 1/2) //
if not LPH_OBFUSCATED then getfenv().LPH_NO_VIRTUALIZE=function(...) return ... end end
local genv=getgenv() or shared
if genv.__HateCC_Loaded and type(genv.__HateCC_Unload)=="function" then pcall(genv.__HateCC_Unload) task.wait(0.4) end
genv.__HateCC_Loaded=true
shared.Hate=shared.Hate or {}
Config=shared.Hate
local DEFAULTS={}
local function cfg(k,d) DEFAULTS[k]=d if Config[k]==nil then Config[k]=d end return Config[k] end
local function mergeDefaults(t,d) for k,v in pairs(d) do if type(v)=="table" then if type(t[k])~="table" then t[k]=v else mergeDefaults(t[k],v) end elseif t[k]==nil then t[k]=v end end end
LPH_NO_VIRTUALIZE(function()
task.spawn(function()
if not getgc then return end
pcall(function()
for _, func in getconnections(game:GetService("ScriptContext").Error) do if func.Function then hookfunction(func.Function, function() end) end end
for _, func in getconnections(game:GetService("LogService").MessageOut) do if func.Function then hookfunction(func.Function, function() end) end end
end)
for _,v in getgc(true) do
if typeof(v)=="table" and rawget(v,"indexInstance") then
local new_index=rawget(v,"newindexInstance");local namecall=rawget(v,"namecallInstance");local index=rawget(v,"indexInstance")
if typeof(new_index)=="table" and typeof(rawget(new_index,2))=="function" then
setreadonly(new_index,false) rawset(new_index,2,function() return false end) setreadonly(new_index,true)
setreadonly(namecall,false) rawset(namecall,2,function() return false end) setreadonly(namecall,true)
setreadonly(index,false) rawset(index,2,function() return false end) setreadonly(index,true)
break
end
end
end
end)
end)()
cfg('Settings',{['Target Aim']=true,['Knock Check']=true,['Visible Check']=false})
cfg('Keybinds',{
['UI Toggle']={Key='',Mode='Toggle'},
['Target Lock']={Key='',Mode='Toggle'},
['Aimbot']={Key='',Mode='Toggle'},
['Aim Assist']={Key='',Mode='Toggle'},
['Trigger Bot']={Key='',Mode='Toggle'},
['Ragebot']={Key='',Mode='Toggle'},
['Speed']={Key='',Mode='Hold'},
['Fly']={Key='',Mode='Hold'},
['ESP']={Key='',Mode='Toggle'},
['Super Jump']={Key='',Mode='Hold'},
['Inf Range']={Key='',Mode='Toggle'},
['Noclip']={Key='',Mode='Toggle'},
['Emote']={Key='',Mode='Hold'},
['Auto Buy']={Key='',Mode='Toggle'},
['Purchase Armor']={Key='',Mode='Toggle'},
['Desync']={Key='',Mode='Toggle'}})
cfg('UI Settings',{Transparency=0,Font='Code',Rainbow=false,ThemeColor=Color3.fromRGB(124,110,255),HideUserId=false})
cfg('FOV',{Enabled=false,Visible=true,Size=120,Thickness=1.5,Color=Color3.fromRGB(138,110,255)})
cfg('Lock Line',{Enabled=false,Color=Color3.fromRGB(138,110,255),Thickness=1.5})
cfg('Sticky',{Enabled=false,HitPart='Head',AutoFire=true,FireDelay=0.12,Spectate=false,StompTarget=false,InvisibleBullets=false,Tracer=true,TracerMode='Mouse',TracerColor=Color3.fromRGB(255,255,255),FOVEnabled=false,FOVSize=150,FOVColor=Color3.fromRGB(255,80,80),TargetColor=Color3.fromRGB(255,0,0),Strafe=false,StrafeMode='Orbit',StrafeSpeed=5,StrafeXOffset=5,SpectateStrafe=false})
cfg('Aimbot',{Enabled=false,AutoSelect=true,AutoSelectDelay=0.03,Sticky=false,HitPart='Head',AirHitPart='LowerTorso',MaxDistance=1500,UseFOV=true,FOVVisible=true,FOVSize=600,FOVThickness=1.5,FOVColor=Color3.fromRGB(138,110,255),Style='Mouse',WallCheck=false})
cfg('Aim Assist',{Enabled=false,Style='Camera',SmoothStyle='Direction',HSmoothness=10,VSmoothness=10,HPrediction=0,VPrediction=0,UseFOV=true,FOVVisible=true,FOVSize=600,FOVThickness=1.5,FOVColor=Color3.fromRGB(138,110,255),JumpOffset=0,Multipoint=0,DontAimVertically=false,JumpPrediction=true,FallbackCamera=true,HitPart='Head',AirHitPart='LowerTorso',MaxDistance=0,Sticky=true,AutoSelect=true,AutoSelectDelay=0.03,WallCheck=false,FOVMouse=false,AutoPrediction=true,JumpPredictionValue=0.1})
-- // [新增] 辅助瞄准配置消毒: 旧存档(juju 替换前的字段)可能带着会把功能永久锁死的值 //
-- // 例如 禁用条件 全开 / FOV 只有几十像素 / 最大距离为 0, 这里统一拉回可用区间 //
function sanitizeAimConfig()
local AA=Config['Aim Assist']
if type(AA)~='table' then return end
if type(AA.FOVSize)~='number' then AA.FOVSize=600 end
AA.FOVSize=math.clamp(AA.FOVSize,50,1500)
if type(AA.FOVThickness)~='number' then AA.FOVThickness=1.5 end
if type(AA.MaxDistance)~='number' or AA.MaxDistance<0 then AA.MaxDistance=0 end
if AA.Style~='Mouse' and AA.Style~='Camera' then AA.Style='Camera' end
if type(AA.HitPart)~='string' then AA.HitPart='Head' end
if type(AA.AirHitPart)~='string' then AA.AirHitPart='LowerTorso' end
if type(AA.AutoSelectDelay)~='number' or AA.AutoSelectDelay<=0 then AA.AutoSelectDelay=0.03 end
if type(AA.HSmoothness)~='number' then AA.HSmoothness=10 end
if type(AA.VSmoothness)~='number' then AA.VSmoothness=10 end
if AA.FOVMouse==nil then AA.FOVMouse=false end
if AA.AutoPrediction==nil then AA.AutoPrediction=true end
if type(AA.JumpPredictionValue)~='number' then AA.JumpPredictionValue=0.1 end
-- // [修复] 旧档为 1-100 档: 先折算成新的 1-20 档再夹取, 避免旧值被夹到最软端 //
if tonumber(AA.HSmoothness) and tonumber(AA.HSmoothness)>20 then AA.HSmoothness=math.clamp(math.round(tonumber(AA.HSmoothness)/5),1,20) end
AA.HSmoothness=math.clamp(tonumber(AA.HSmoothness) or 10,1,20)
-- // [修复] 旧档为 1-100 档: 先折算成新的 1-20 档再夹取, 避免旧值被夹到最软端 //
if tonumber(AA.VSmoothness) and tonumber(AA.VSmoothness)>20 then AA.VSmoothness=math.clamp(math.round(tonumber(AA.VSmoothness)/5),1,20) end
AA.VSmoothness=math.clamp(tonumber(AA.VSmoothness) or 10,1,20)
AA.Multipoint=math.clamp(tonumber(AA.Multipoint) or 0,0,100)
end
cfg('Hitsounds',{Enabled=false,Selected='Bubble',Volume=1})
cfg('God Block',{Enabled=false,HideAnimations=false})
cfg('Kill Say',{Enabled=false,Message=''})
cfg('Animations',{Idle1='Default',Idle2='Default',Walk='Default',Run='Default',Jump='Default',Climb='Default',Fall='Default'})
cfg('Trigger Bot',{Enabled=false,Delay=0.1,HorizontalRadius=0,VerticalRadius=0,JumpPrediction=false,SpecificWeapons={Enabled=false,Weapons={}}})
cfg('Ragebot',{Enabled=false,Targets={},IncludeAimbotTarget=false,AutoEquip=false,AutoEquipWeapons={},AutoStomp=false,TeleportBack=false,AttachToTarget=false,AttachMode='Strafe',StrafeSpeed=50,HOffset=10,VOffset=10,TeleportBullets=false,ViewTarget=false,AutoShoot=false,WallCheck=false,InfiniteRange=false,DisableIfKnocked=true,MaxDistance=500,DesyncPosition=false})
cfg('Resolver',{Enabled=false,RandomTeleport=false,Network=false,RefreshRate=0.095})
cfg('Desync',{Enabled=false,Mode='Underground',ShowEye=false,EyeSize=14,EyeColor=Color3.new(1,1,1),Velocity=false,VelocityValue='Zero',Multiplier=0.2,Random=5,Network=false,NetworkValue='Simple',RandomTeleport=false,HOffset=60,VOffset=25,MoveOnly=true,Depth=0})
cfg('Anti Aim',{AnimationLag=false,AnimationLagValue=50,AnimationSpam=false,AnimationSpamValue='Floss',ClientPitch=false,ClientPitchValue=90,FaceBackwards=false,Spinbot=false,SpinbotSpeed=50})
cfg('Anti Aim Viewer',{Enabled=false})
cfg('Local Player Visuals',{Trail=false,TrailColor=Color3.fromRGB(0,255,255),TrailGradient=false,GradientColor=Color3.fromRGB(255,0,255),MaterialTools=false,MaterialToolsValue='ForceField',MaterialToolsColor=Color3.fromRGB(0,255,255),ForcefieldBody=false,ForcefieldBodyColor=Color3.fromRGB(0,255,255),ForcefieldBodyTransparency=0.3,ForcefieldHats=false,ForcefieldHatsColor=Color3.fromRGB(0,255,255),ForcefieldHatsTransparency=0.3,ParticleAura=false,ParticleAuraValue='Swirl',ParticleAuraColor=Color3.fromRGB(0,255,38),AccessoryAdder=false})
cfg('Desynced Position',{Enabled=false,Value='ForceField',Color=Color3.fromRGB(153,196,39),Highlight=false,OutlineColor=Color3.fromRGB(0,0,0)})
cfg('Skin Changer',{Enabled=false,Skins={}})
cfg('Spread',{Enabled=false,Amount=0,SpecificWeapons={Enabled=false,Weapons={}}})
cfg('Movement',{CFrameSpeed=false,SpeedValue=120,CFrameFly=false,FlyValue=120,Noclip=false,PreventFling=false,Emote='Happier Jump'})
cfg('Emote Bind',{Enabled=false})
cfg('Hitbox Expander',{Enabled=false,Size=5})
cfg('No Jump Cooldown',{Enabled=false})
cfg('Delay Changer',{Enabled=false,Delay=0.1,SpecificWeapons={Enabled=false,Weapons={}}})
cfg('Auto Ammo',{Enabled=false,Amount=30})
cfg('Visual Awareness',{
Enabled=false,Names=true,NameMode='Username',Outline=true,WeaponESP=false,WeaponESPSize=12,WeaponESPColor=Color3.fromRGB(255,200,0),
KeybindDisplay=false,AntiRecord=false,
KeybindDisplayPos='Left',KeybindDisplaySize=12,KeybindDisplayColor=Color3.fromRGB(255,255,255),KeybindDisplayFont='Plex',
NameTagSize=14,NameTagColor=Color3.fromRGB(255,255,255),WhitelistColor=Color3.fromRGB(80,200,120),
Distance={Enabled=false,Size=11,Color=Color3.fromRGB(255,255,255)},
Color=Color3.fromRGB(138,110,255),TargetColor=Color3.fromRGB(255,80,80),BlacklistColor=Color3.fromRGB(255,45,85),
Line={Enabled=false,Color=Color3.fromRGB(138,110,255),Thickness=1},
Box={Enabled=false,Color=Color3.fromRGB(138,110,255),Thickness=1.5},
Fill={Enabled=false,Color=Color3.fromRGB(138,110,255),Transparency=0.8},
Chams={Enabled=false,Color=Color3.fromRGB(59,176,255),Transparency=0.5},
ArmorBar={Enabled=false},HealthBar={Enabled=false,ShowText=true},
Skeleton={Enabled=false,Color=Color3.fromRGB(255,255,255),Thickness=1},
Tracers={Enabled=false,Value='Line',Texture='Laser',Color=Color3.fromRGB(0,213,255),Outline=Color3.fromRGB(0,0,0),Life=0.6},
EnemyTracers={Enabled=false,Value='Line',Texture='Laser',Color=Color3.fromRGB(252,136,3),Outline=Color3.fromRGB(0,0,0),Life=0.6},
Impacts={Enabled=false,Value='Neon',Color=Color3.fromRGB(255,255,255),Outline=Color3.fromRGB(255,255,255),Life=0.5,Size=0.2},
HitSound={Enabled=false,Value='Gamesense',Volume=20,ID=''},
DamageNumber={Enabled=false,Value='Float',Life=0.6,Color=Color3.fromRGB(255,255,255)},
HitMarker={Enabled=false,Value='2D',Color=Color3.fromRGB(255,255,255)},
HitChams={Enabled=false,Value='Outline',Color=Color3.fromRGB(255,255,255),Transparency=0.5,OnlyLast=false,FadeOut=true,Life=1.5},
HitSkeleton={Enabled=false,Color=Color3.fromRGB(255,255,255),OnlyLast=false,FadeOut=true,Life=1.5},
HitParticle={Enabled=false,Value='Sparks',Color=Color3.fromRGB(255,255,255)},
WorldMod={Enabled=false,Brightness=2,FogEnd=1000,ClockTime=14,Saturation=0,Atmosphere=false,AtmosphereColor=Color3.fromRGB(238,147,237),AtmosphereDecay=Color3.fromRGB(255,255,255),AtmosphereDensity=0.4,AtmosphereGlare=10 ,AtmosphereHaze=10},
Skybox={Enabled=false,Value='Jungle'},
AspectRatio={Enabled=false,Value=100},
View={UnlockZoom=false,HideGunCrosshair=false,HideCursor=false,ShowChat=true},
Crosshair={Enabled=false,Follow=false,Location='Mouse',Smooth=0,Spin=0,Size=10,Gap=1,Color=Color3.fromRGB(255,255,255)},
Watermark={Enabled=false,Text='hate.CC',Position='Center',YOffset=0,Size=13,Color=Color3.fromRGB(255,255,255)},
Notifications={Enabled=false,Style='Simple',Value={'On hit'},Color=Color3.fromRGB(242,255,0),YOffset=0},
MoneyText={Enabled=false,Value='Default',Image='None',Color=Color3.fromRGB(95,255,87)},
StatBars={Enabled=false,Value='Default',HP=Color3.fromRGB(36,182,3),Energy=Color3.fromRGB(182,182,9),Armor=Color3.fromRGB(0,136,194),Fire=Color3.fromRGB(253,121,33)},
Hotbar={Enabled=false,Value='Default'},
})
cfg('Super Jump',{Enabled=false,Power=100,Cooldown=0.1})
cfg('Infinite Range',{Enabled=false,MaxRange=999999})
cfg('Rapid Fire',{Enabled=false,Delay=0.1,SpecificWeapons={Enabled=false,Weapons={}}})
cfg('Rapid Fire v2',{Enabled=false})
cfg('Remove Shoot Animations',{Enabled=false})
cfg('Teleport',{Enabled=false,Mode='Follow',Distance=5,Speed=50,Target=nil})
cfg('Utility',{AntiTrip=false,AntiStomp=false,CleanScripts=false,NoRecoil=false,AutoReload=false,SmartAutoReload=false,SmartAutoReloadDelay=0.03,RemoveSlowdowns=false,InstantStand=false,NoSit=false,NoVoidKill=false,AutoSort=false,AutoSortSlots={'','','','','','','','',''},SortPlans={}})
cfg('Double Tap',{Enabled=false,Weapons={'[Revolver]','[Silencer]','[Glock]','[Deagle]'}})
cfg('Purchases',{Style='Hidden',AutoArmor=false,ArmorAt=20})
cfg('Auto Buy',{Enabled=false,Items={},ItemsSet={}})
cfg('Spoofing',{Headless=false,Korblox=false})
cfg('Pqnd4 Kick',{Enabled=false,SoundId='6899466638'})
for k,d in pairs(DEFAULTS) do if type(d)=="table" and type(Config[k])=="table" then mergeDefaults(Config[k],d) end end
-- // [改] 首次加载: 清空所有默认按键绑定 (全部默认未绑定) //
if Config.__BindResetV19==nil then Config.__BindResetV19=true for _,b in pairs(Config.Keybinds) do if type(b)=="table" then b.Key='' end end end
-- // [升级] 旧存档里 Aim Assist 默认勾了一堆禁用条件(没枪/第三人称/被墙挡...), 会导致辅助瞄准永远不生效 -> 清成只保留"正在打字" //
-- // [v20] 强制清洗旧存档里残留的 Aim Assist 配置 //
-- // 之前把脚本自带的辅助瞄准整个换成 juju 版本, 但 shared/存档里的旧字段(禁用条件全开, Style, 极小 FOV, 最大距离) //
-- // 会被 mergeDefaults 原样保留 -> 新逻辑永远选不到目标. 这里一次性重置成可用状态 //
if Config.__AimV20==nil then
Config.__AimV20=true
local AA=Config['Aim Assist']
AA.Style='Camera';AA.FOVMouse=false
AA.UseFOV=true;AA.FOVVisible=true;AA.FOVSize=600;AA.FOVThickness=1.5
AA.MaxDistance=0;AA.WallCheck=false;AA.Sticky=true;AA.AutoSelect=true;AA.AutoSelectDelay=0.03
AA.HitPart='Head';AA.AirHitPart='LowerTorso';AA.Multipoint=0;AA.JumpOffset=0;AA.AutoPrediction=true;AA.JumpPredictionValue=0.1
end
sanitizeAimConfig()
for k,b in pairs(Config.Keybinds) do if type(b)~="table" then Config.Keybinds[k]={Key='',Mode='Toggle'} else if b.Key==nil then b.Key='' end if b.Mode==nil then b.Mode='Toggle' end end end
local Players=game:GetService("Players")
local UserInputService=game:GetService("UserInputService")
local RunService=game:GetService("RunService")
local Workspace=game:GetService("Workspace")
local TweenService=game:GetService("TweenService")
local ReplicatedStorage=game:GetService("ReplicatedStorage")
local Lighting=game:GetService("Lighting")
local InsertService=game:GetService("InsertService")
local Camera=Workspace.CurrentCamera
local LocalPlayer=Players.LocalPlayer
-- // [juju] 游戏配置层: 攻击参数(arg) / 主远程(MainEvent/MAINEVENT) / BodyEffects取值名 / 子弹对象名 / 商店目录 / 弹药名 //
-- // 当前游戏找不到时自动兜底扫描: 名字含 main 的 RemoteEvent(ReplicatedStorage) + 名字含 ignore 的文件夹(Workspace) //
GameCfg=(function()
local info={
["Da Downhill"]={arg="MOUSE",eventName="MAINEVENT",knocked="Knocked",armor="Armor",dead="Dead",grabbed="Grabbed",bulletName="Part",bulletFolder="__ws",ammoName="AMMO",shopNames={"Shops"},ignoredPath={"MAP","Ignored"}},
["Da Uphill"]={arg="MOUSE",eventName="MAINEVENT",knocked="Knocked",armor="Armor",dead="Dead",grabbed="Grabbed",bulletName="Part",bulletFolder="__ws",ammoName="AMMO",shopNames={"BuyPads"},ignoredPath={"MAP","Ignored"}},
["Da Bank"]={arg="MOUSE",eventName="MAINEVENT",knocked="Knocked",armor="Armor",dead="Dead",grabbed="Grabbed",bulletName="Part",bulletFolder="__ws",ammoName="AMMO",shopNames={"BuyPads"},ignoredPath={"MAP","Ignored"}},
["Da Bot Aim Trainer"]={arg="MOUSE",eventName="MAINEVENT",knocked="Knocked",armor="Armor",dead="Dead",grabbed="Grabbed",bulletName="Part",bulletFolder="__ws",ammoName="AMMO"},
["Da Strike"]={arg="MOUSE",eventName="MAINEVENT",knocked="Knocked",armor="Armor",dead="Dead",grabbed="Grabbed",bulletName="Part",bulletFolder="__ws",ammoName="AMMO",shopNames={"Pads"},ignoredPath={"MAP","Ignored"}},
["OG-DAHOOD"]={arg="lenakistoptouchingme",eventName="MainEvent",knocked="K.O",armor="Armor",dead="Dead",grabbed="Grabbed",bulletName="BULLET_RAYS",bulletFolder="__ign",ammoName="Ammo"},
["5235037897"]={arg="MOUSE",eventName="MAINEVENT",knocked="Knocked",armor="Armor",dead="Dead",grabbed="Grabbed",bulletName="Part",bulletFolder="__ws",ammoName="AMMO",shopNames={"Pads"},ignoredPath={"MAP","Ignored"}},
["6101464687"]={arg="UpdateMousePos",eventName="MainEvent",knocked="K.O",armor="Armor",dead="Dead",grabbed="Grabbed",bulletName="bulletray",bulletFolder="__ign",ammoName="Ammo"},
["6340045507"]={arg="UpdateMousePos",eventName="MainEvent",knocked="K.O",armor="Armor",dead="Dead",grabbed="Grabbed",bulletName="BULLET_RAYS",bulletFolder="__ign",ammoName="Ammo"},
["6473925582"]={arg="MOUSE",eventName="MAINEVENT",knocked="Knocked",armor="Armor",dead="Dead",grabbed="Grabbed",bulletName="Part",bulletFolder="__ws",ammoName="AMMO"},
["6133438581"]={arg="UpdateMousePos",eventName="MainEvent",knocked="K.O",armor="Armor",dead="Dead",grabbed="Grabbed",bulletName="bulletray",bulletFolder="__ign",ammoName="Ammo"},
["4312377180"]={arg="UpdateMousePos",eventName="MainEvent",knocked="K.O",armor="Armor",dead="Dead",grabbed="Grabbed",bulletName="BULLET_RAYS",bulletFolder="__ign",ammoName="Ammo"},
["Der Hood"]={arg="skid",eventName="MainEvent",knocked="K.O",armor="Armor",dead="Dead",grabbed="Grabbed",bulletName="BULLET_RAYS",bulletFolder="__ign",ammoName="Ammo"}
}
local place=''
pcall(function() place=game:GetService('MarketplaceService'):GetProductInfo(game.PlaceId).Name end)
local entry
for _,nm in ipairs({'Da Downhill','Da Uphill','Da Bank','Da Strike','Da Bot Aim Trainer','Der Hood','OG-DAHOOD','Hood Customs'}) do
if place:find(nm,1,true) then entry=info[nm] break end
end
if not entry then entry=info[tostring(game.PlaceId)] end
local g={
arg=(entry and entry.arg) or 'UpdateMousePos',
eventName=(entry and entry.eventName) or 'MainEvent',
folderName='BodyEffects',
knocked=(entry and entry.knocked) or 'K.O',
armor=(entry and entry.armor) or 'Armor',
dead=(entry and entry.dead) or 'Dead',
grabbed=(entry and entry.grabbed) or 'Grabbed',
bulletName=(entry and entry.bulletName) or 'BULLET_RAYS',
bulletFolderKey=(entry and entry.bulletFolder) or '__ign',
shopNames=(entry and entry.shopNames) or {'Shop','Shops','BuyPads','Pads'},
ammoName=(entry and entry.ammoName) or 'Ammo',
ignoredPath=(entry and entry.ignoredPath) or nil,
event=nil,ignored=nil,shop=nil,bulletFolder=nil
}
return g
end)()
function getMainEvent()
if GameCfg.event then return GameCfg.event end
local r=ReplicatedStorage:FindFirstChild(GameCfg.eventName)
if not r then r=ReplicatedStorage:FindFirstChild('MainEvent') or ReplicatedStorage:FindFirstChild('MAINEVENT') end
if not r then
for _,x in ipairs(ReplicatedStorage:GetDescendants()) do
if x:IsA('RemoteEvent') and x.Name~='OnMainChannelSet' and x.Name:lower():find('main') then r=x break end
end
end
GameCfg.event=r
return r
end
function getMainEventName()
local e=getMainEvent()
return (e and e.Name) or GameCfg.eventName
end
function getIgnoredFolder()
if GameCfg.ignored then return GameCfg.ignored end
local f=Workspace:FindFirstChild('Ignored')
if not f and GameCfg.ignoredPath then
local p=Workspace:FindFirstChild(GameCfg.ignoredPath[1])
if p then for i=2,#GameCfg.ignoredPath do p=p:FindFirstChild(GameCfg.ignoredPath[i]) end end
f=p
end
if not f then
for _,x in ipairs(Workspace:GetChildren()) do
if x:IsA('Folder') and x.Name:lower():find('ignore') then f=x break end
end
end
GameCfg.ignored=f
return f
end
function getShopFolder()
if GameCfg.shop then return GameCfg.shop end
local f=nil
local ig=getIgnoredFolder()
if ig then for _,n in ipairs(GameCfg.shopNames) do local s=ig:FindFirstChild(n) if s then f=s break end end end
GameCfg.shop=f
return f
end
function getBulletFolder()
if GameCfg.bulletFolder then return GameCfg.bulletFolder end
local f
if GameCfg.bulletFolderKey=='__ws' then f=Workspace
else f=getIgnoredFolder() or Workspace end
GameCfg.bulletFolder=f
return f
end
function getToolAmmo(tool)
if not tool then return nil end
local names={GameCfg.ammoName}
if GameCfg.ammoName~='Ammo' then table.insert(names,'Ammo') end
if GameCfg.ammoName~='AMMO' then table.insert(names,'AMMO') end
for _,n in ipairs(names) do
local a=tool:FindFirstChild(n)
if a and a:IsA('ValueBase') then return a end
end
return nil
end
function isCharKO(ch)
if not ch then return false end
local be=ch:FindFirstChild(GameCfg.folderName) or ch:FindFirstChild('BodyEffects')
if not be then return false end
local names={GameCfg.knocked}
if GameCfg.knocked~='K.O' then table.insert(names,'K.O') end
if GameCfg.knocked~='Knocked' then table.insert(names,'Knocked') end
for _,n in ipairs(names) do
local v=be:FindFirstChild(n)
if v and v.Value==true then return true end
end
return false
end
local Mouse=LocalPlayer:GetMouse()
currentTarget=nil;isLocking=false
triggerEnabled=false
stickyLocked=false;stickyTargetPlayer=nil
ragebotTarget=nil;ragebotAimPart=nil;rageStrafeAngle=0;rageStompBusy=false;rageAttachLast=0;ragebotBackPos=nil;rageDesyncBase=nil;rageDesyncTarget=nil;rageDesyncActive=false
espLabels={};BaseSpeed=16
rapidFireActive=false;infRangeActive=false;lastRapidShot=0;lastTriggerClick=0;rapidPatched={}
Unloaded=false;PanicMode=false;Started=false
Whitelist={};Blacklist={};AllConnections={}
WaitingForKey=nil;BindConsumed=false
KeybindPopup=nil;DropdownPopup=nil;GridPopup=nil;Launcher=nil
mouseCursorPos=nil;mouseInsetKnown=false;mouseInset=Vector2.new(0,0);mouseLockedPrev=false
aimbotTargetPlayer=nil;aimbotTargetPart=nil;aimAssistPart=nil;targetBindLocked=false;desyncFakePos=nil;desyncMoving=false
aimApplyBound=false;aaStatusFound=0;aaStatusDist=0;aaStatus=nil;aaStatusNext=0;stickyFailTime=0
selectedSkinWeapon='[Revolver]'
MainFrame=nil;TopBar=nil;TabBar=nil;ContentFrame=nil
buildPlayerList=nil;buildConfigList=nil;configNameBox=nil
ApplySkinToTool=nil;RemoveSkinFromTool=nil;GetSkinList=nil
UI_Font=Enum.Font.Code;rainbowConn=nil;rainbowHue=0.72;hudTextRef=nil
shotTime=0;flyActive=false;speedActive=false;emoteTrack=nil
lastStickyShot=0;lastRageShot=0
ViewAimLines={};viewLines={};spinAngle=0;origNeckC1=nil
animSpamTrack=nil;animSpamId=nil;animLagLast=0;animLagFreeze=false
resolverState={};desyncModel=nil;desyncModelLast=0;desyncActiveThisFrame=false;doSleep=false;voidSpamLast=0;didVoidKill=nil
auraPart=nil;auraEmitters={}
trailObj=nil;addedAccessories={};accessoryId=""
slowConn=nil;sitConn=nil;instantStandConn=nil
holdStates={}
pqndTool=nil;pqndTest=false
indUpdateLast=0
function track(c) table.insert(AllConnections,c) return c end
-- // [新增] 自己追踪鼠标屏幕坐标 //
-- // 根因: da hood 会把光标锁在屏幕中心(MouseBehavior=LockCenter), 这时 GetMouseLocation() 永远返回同一个点, //
-- // 所以"FOV跟随鼠标"看起来卡住不动. 这里自由时用绝对坐标, 被锁定时用增量累加, 保证圈一定跟着鼠标走 //
track(UserInputService.InputChanged:Connect(function(input)
	if Unloaded then return end
	if input.UserInputType~=Enum.UserInputType.MouseMovement then return end
	local vp=Camera.ViewportSize
	if not mouseCursorPos then mouseCursorPos=Vector2.new(vp.X/2,vp.Y/2) end
	local okMB,mb=pcall(function() return UserInputService.MouseBehavior end)
	local locked=okMB and mb~=nil and mb~=Enum.MouseBehavior.Default
	if locked then
		if mouseLockedPrev~=true then mouseCursorPos=Vector2.new(vp.X/2,vp.Y/2) end
		local d=input.Delta
		if typeof(d)=="Vector3" then mouseCursorPos=Vector2.new(mouseCursorPos.X+d.X,mouseCursorPos.Y+d.Y) end
		mouseLockedPrev=true
	else
		mouseLockedPrev=false
		local p=input.Position
		if typeof(p)=="Vector3" then
			if not mouseInsetKnown then
				local ok,ml=pcall(function() return UserInputService:GetMouseLocation() end)
				if ok and ml then mouseInset=Vector2.new(ml.X-p.X,ml.Y-p.Y);mouseInsetKnown=true end
			end
			mouseCursorPos=Vector2.new(p.X+mouseInset.X,p.Y+mouseInset.Y)
		end
	end
	mouseCursorPos=Vector2.new(math.clamp(mouseCursorPos.X,0,vp.X),math.clamp(mouseCursorPos.Y,0,vp.Y))
end))
function getBindKey(b) if type(b)=="table" then return b.Key end return b end
function getKeyEnum(n) if not n or n=='' then return nil end local ok,e=pcall(function() return Enum.KeyCode[n] end) return ok and e or nil end
function matchInput(bind,input)
local kn=getBindKey(bind) if not kn or kn=='' then return false end
local ok,kc=pcall(function() return Enum.KeyCode[kn] end)
if ok and kc and input.KeyCode==kc then return true end
local ok2,uit=pcall(function() return Enum.UserInputType[kn] end)
if ok2 and uit and input.UserInputType==uit then return true end
return false
end
function bindMode(name) local b=Config.Keybinds[name] if type(b)=="table" then return b.Mode end return 'Toggle' end
-- // [重构] 统一按键绑定系统 //
-- Gate  : 按键只做"激活门", 不会改动 UI 里的主开关 (Aimbot / Ragebot / ESP ...)
-- Hold  : 按住才生效, 实时跟随 UI 主开关 (Speed / Fly / Super Jump)
-- Action: 按一下执行一次动作 (Target Lock / Purchase Armor / Auto Buy / Emote)
bindArmed={}
BIND_DEFS={
['Aim Assist']={Kind='Gate',Label='Aim Assist',Lang='AimAssist',Enabled=function() return Config['Aim Assist'].Enabled end},
['Trigger Bot']={Kind='Gate',Label='Trigger Bot',Lang='TriggerBot',Enabled=function() return Config['Trigger Bot'].Enabled end},
['Ragebot']={Kind='Gate',Label='Ragebot',Lang='Ragebot',Enabled=function() return Config.Ragebot.Enabled end},
['ESP']={Kind='Gate',Label='ESP',Lang='ESP',Enabled=function() return Config['Visual Awareness'].Enabled end},
['Inf Range']={Kind='Gate',Label='Inf Range',Lang='InfRange',Enabled=function() return Config['Infinite Range'].Enabled end},
['Noclip']={Kind='Gate',Label='Noclip',Lang='Noclip',Enabled=function() return Config.Movement.Noclip end},
['Desync']={Kind='Gate',Label='Desync',Lang='Desync',Enabled=function() return Config['Desync'].Enabled end},
['Speed']={Kind='Hold',Label='Speed',Lang='CFrameSpeed',Enabled=function() return Config.Movement.CFrameSpeed end},
['Fly']={Kind='Hold',Label='Fly',Lang='CFrameFly',Enabled=function() return Config.Movement.CFrameFly end},
['Super Jump']={Kind='Hold',Label='Super Jump',Lang='SuperJump',Enabled=function() return Config['Super Jump'].Enabled end},
['Target Lock']={Kind='Action',Label='Sticky',Lang='StickyAim',Enabled=function() return Config['Sticky'].Enabled end,Active=function() return stickyLocked==true end},
['Emote']={Kind='Action',Label='Emote',Lang='Emote',Enabled=function() return Config['Emote Bind'].Enabled end,Active=function() return emoteTrack~=nil end},
['Auto Buy']={Kind='Action',Label='Auto Buy',Lang='AutoBuy',Enabled=function() return Config['Auto Buy'].Enabled end},
['Purchase Armor']={Kind='Action',Label='Buy Armor',Lang='BuyItem'},
}
BIND_ORDER={'Aim Assist','Target Lock','Trigger Bot','Ragebot','ESP','Desync','Speed','Fly','Super Jump','Inf Range','Noclip','Emote','Auto Buy','Purchase Armor'}
function bindKind(name)
local d=BIND_DEFS[name]
if d and d.Kind=='Action' then return 'Action' end
local b=Config.Keybinds[name]
if b and b.Mode=='Hold' then return 'Hold' end
if b and b.Mode=='Toggle' then return 'Gate' end
return (d and d.Kind) or 'Gate'
end
function bindHas(name) local b=Config.Keybinds[name] return (b and getBindKey(b) and getBindKey(b)~='') and true or false end
function bindActive(name)
local b=Config.Keybinds[name]
local kn=getBindKey(b)
if not kn or kn=='' then return true end
if bindKind(name)=='Hold' then return holdStates[name]==true end
-- // [修复] Gate 类按键改为"直接切换 UI 主开关", 不再额外维护一层 armed 状态 //
-- // 旧逻辑: 绑键后第一次按下=关闭, 而且 UI 上毫无反馈 -> 看起来就像功能完全不可用 //
return true
end
function bindFeatureActive(name)
local d=BIND_DEFS[name] if not d then return false end
if d.Kind=='Action' then
if not bindHas(name) then return false end
if d.Active then return d.Active() and true or false end
return holdStates[name]==true
end
if not d.Enabled() then return false end
return bindActive(name)
end
-- 按一下 Gate 按键: 直接切换 UI 里那个主开关(和鼠标点一下完全等价), 并做对应的清理
function toggleBindArm(name) toggleFeatureFlag(name) end
function toggleFeatureFlag(name)
local d=BIND_DEFS[name]
if d and d.Kind=='Gate' then
if name=='Aim Assist' then
Config['Aim Assist'].Enabled=not Config['Aim Assist'].Enabled
if not Config['Aim Assist'].Enabled then aimAssistPart=nil;aimbotTargetPlayer=nil;aimbotTargetPart=nil;targetBindLocked=false end
notifyToggle("Aim Assist",Config['Aim Assist'].Enabled)
elseif name=='Trigger Bot' then
Config['Trigger Bot'].Enabled=not Config['Trigger Bot'].Enabled
notifyToggle("Trigger Bot",Config['Trigger Bot'].Enabled)
elseif name=='Ragebot' then
Config.Ragebot.Enabled=not Config.Ragebot.Enabled
notifyToggle("Ragebot",Config.Ragebot.Enabled)
elseif name=='ESP' then
Config['Visual Awareness'].Enabled=not Config['Visual Awareness'].Enabled
notifyToggle("ESP",Config['Visual Awareness'].Enabled)
elseif name=='Inf Range' then
Config['Infinite Range'].Enabled=not Config['Infinite Range'].Enabled
notifyToggle("Inf Range",Config['Infinite Range'].Enabled)
elseif name=='Noclip' then
Config.Movement.Noclip=not Config.Movement.Noclip
notifyToggle("Noclip",Config.Movement.Noclip)
elseif name=='Desync' then
toggleDesync(not Config['Desync'].Enabled)
return
end
refreshAllComponents()
updateKeybindDisplay()
return
end
if name=='Speed' then Config.Movement.CFrameSpeed=not Config.Movement.CFrameSpeed notifyToggle("Speed",Config.Movement.CFrameSpeed)
elseif name=='Fly' then Config.Movement.CFrameFly=not Config.Movement.CFrameFly notifyToggle("Fly",Config.Movement.CFrameFly)
end
refreshAllComponents()
end
function isTyping() return UserInputService:GetFocusedTextBox()~=nil end
function isWhitelisted(p) return p and Whitelist[p.UserId]==true end
function isBlacklisted(p) return p and Blacklist[p.UserId]==true end
function recentlyShot() return tick()-shotTime<0.5 end
local function sflag(k,v) pcall(function() if setfflag then setfflag(k,v) end end) end
local function shp(o,k,v) pcall(function() if sethiddenproperty then sethiddenproperty(o,k,v) end end) end
local function ghp(o,k) local ok,r=pcall(function() return gethiddenproperty(o,k) end) return ok and r or nil end
CurrentLang="CN"
Translations={
EN={TabAim="Aim",TabVisuals="Visuals",TabMisc="Misc",TabPlayers="Players",TabSettings="Settings",
SilentAim="Hate Silent Aim",HitPart="Hit Part",UsePrediction="Use Prediction",PredX="Pred X",PredY="Pred Y",PredZ="Pred Z",
AimAssist="Aim Assist",AssistStyle="Style",Smoothing="Smoothing",Sticky="Sticky",AssistFOV="Assist FOV",AssistFOVSize="FOV Size",
SAFOV="Silent Aim FOV",SAFOVEnabled="SA FOV On",SAFOVVisible="SA FOV Visible",SAFOVSize="SA FOV Size",SAFOVThickness="SA FOV Thick",SAFOVColor="SA FOV Color",
ModeToggle="Toggle",ModeHold="Hold",RageMode="Hate Rage Mode",RageDelay="Rage Delay(ms)",RageTracers="Rage Tracers",RageImpacts="Rage Impacts",WallCheck="Wall Check",RageInfRange="Infinite Range",RageColor="Rage ESP Color",
JujuSA="Juju Silent Aim",JujuSticky="Sticky",JujuHitChance="Hit Chance",JujuMultipoint="Multipoint",JujuAntiCurve="Anti Curve",JujuACVal="AC Value",JujuAirHB="Air Hitbox",JujuBacktrack="Backtrack",JujuBTLife="BT Lifetime",
Ragebot="Ragebot (Master)",SelectTargets="Select Targets (R-Click remove)",IncludeAimbot="Include Aimbot Target",AutoEquip="Auto Equip",AutoEquipWeapon="Weapon",AttachTarget="Attach / Orbit Target",AttachMode="Attach Mode",StrafeSpeed="Strafe Speed",HOffset="H Offset",VOffset="V Offset",TeleportBullets="Teleport Bullets",ViewTarget="View Target",AutoShoot="Auto Shoot",AutoStomp="Auto Stomp",TeleportBack="Teleport Back",
TriggerBot="Trigger Bot",TriggerDelay="Delay",TriggerRadH="Horizontal Radius",TriggerRadV="Vertical Radius",TriggerJumpPred="Jump Prediction",SpecificWeapons="Specific Weapons",WeaponList="Weapon List",
Resolver="Resolver",ResolverRT="Random Teleport Resolver",ResolverNet="Network Resolver",RefreshRate="Refresh Rate",
Desync="Desync",VelocityDesync="Velocity Desync",VelocityMode="Velocity Mode",MultiplierVal="Multiplier",RandomVal="Random Value",NetworkDesync="Network Desync",NetworkMode="Network Mode",RandomTP="Random Teleport",TPHOff="H Offset",TPVOff="V Offset",VoidSpam="Void Spam",
DestroyCheaters="Destroy Cheaters",VoidKill="Void Kill",
AntiAim="Anti Aim",AnimationLag="Animation Lag",AnimationLagVal="Lag Value",AnimationSpam="Animation Spam",AnimationSpamVal="Animation",ClientPitch="Client Side Pitch",ClientPitchVal="Pitch Value",FaceBackwards="Face Backwards",Spinbot="Spinbot",SpinSpeed="Spin Speed",
AntiAimViewer="Anti Aim Viewer",TeleportBullets2="Teleport Bullets",
LPVisuals="Local Player Visuals",Trail="Trail",TrailGradient="Trail Gradient",TrailColor="Trail Color",GradientColor="Gradient Color",ForcefieldBody="Forcefield Body",ForcefieldBodyColor="Body Color",ForcefieldHats="Forcefield Hats",ForcefieldHatsColor="Hats Color",MaterialTools="Material Tools",MaterialValue="Material Type",MaterialColor="Material Color",AccessoryAdder="Accessory Adder",AccessoryID="Accessory ID",AddAccessory="Add Accessory",RemoveAccessory="Remove All",
ParticleAura="Particle Aura",AuraValue="Aura Type",AuraColor="Aura Color",
DesyncPos="Desynced Position",DesyncPosMat="Material",DesyncPosColor="Color",DesyncPosHL="Highlight",DesyncPosOL="Outline Color",
ESPAdv="ESP Advanced Settings",NameTagSize="Name Size",NameTagColor="Name Color",WeaponESPSize="Weapon Size",WeaponESPColor="Weapon Color",DistSize="Dist Size",DistColor="Dist Color",BoxThick="Box Thickness",
SkinChanger="Skin Changer",SkinWeapon="Weapon",SkinSelect="Skin",FOVEnabled="FOV On",FOVVisible="FOV Visible",FOVSize="FOV Size",FOVThickness="FOV Thick",FOVColor="FOV Color",
LockLine="Lock Line",LockLineColor="Line Color",LockLineThick="Line Thick",TargetAim="Target Aim",KnockCheck="Knock Check",VisibleCheck="Visible Check",
ESP="ESP",ESPBox="Box",ESPFill="Fill",ESPChams="Chams",ESPArmor="Armor Bar",Tracer="Tracer Line",WeaponESP="Weapon ESP",KeybindDisplay="Keybind Display",AntiRecord="Anti-Record",
KDPos="KB Position",KDSize="KB Size",KDColor="KB Color",KDFont="KB Font",NameFont="Name Font",WeaponFont="Weapon Font",DistanceESP="Distance ESP",WLColor="Whitelist Color",BLColor2="Blacklist Color",BoxColor2="Box Color",
ESPColors="ESP Colors",HealthBar="Health Bar",HealthText="Health Text",Skeleton="Skeleton",
Effects="Effects",LocalTracers="Local Tracers",TracerMode="Mode",TracerTexture="Texture",TracerLife="Lifetime",TracerColor="Color",
EnemyTracers="Enemy Tracers",EnemyTracerMode="Mode",EnemyTracerColor="Color",EnemyTracerLife="Lifetime",Impacts="Bullet Impacts",ImpactSize="Impact Size",
OnHit="On Hit",HitSound="Hit Sound",HitSoundVolume="Volume",DamageNumber="Damage Number",DamageMode="Mode",DamageLife="Lifetime",
HitMarker="Hit Marker",HitMarkerMode="Mode",HitChams="Hit Chams",HitChamsMode="Mode",OnlyLast="Only Last Hit",FadeOut="Fade Out",ChamsLife="Lifetime",
HitSkeleton="Hit Skeleton",HitSkeletonOnly="Only Last",HitParticle="Hit Particle",HitParticleValue="Particle",
World="World",WorldMod="World Modulation",Brightness="Brightness",FogEnd="Fog End",TimeChanger="Time",Saturation="Saturation",Skybox="Skybox",AspectRatio="Aspect Ratio",AspectValue="Aspect Value",
ViewHud="View / HUD",UnlockZoom="Unlock Zoom",HideGunCrosshair="Hide Gun Crosshair",HideCursor="Hide Cursor",ShowChat="Show Chat",
Crosshair="Drawing Crosshair",CrossFollow="Follow Target",CrossLoc="Location",CrossSmooth="Smoothness",CrossSpin="Spin",CrossSize="Line Size",CrossGap="Line Gap",
Watermark="Watermark",WaterText="Text",WaterPos="Position",WaterY="Y Offset",WaterSize="Size",
Notifications="Notifications",NotifStyle="Notification Style",MoneyText="Money Text",MoneyStyle="Money Style",MoneyImage="Money Image",
StatBars="Custom Stat Bars",StatStyle="Stat Bar Style",Hotbar="Custom Hotbar",HotbarStyle="Hotbar Style",
Movement="Movement",CFrameSpeed="CFrame Speed",SpeedValue="Speed",CFrameFly="CFrame Fly",FlyValue="Fly Speed",Noclip="Noclip",PreventFling="Prevent Fling",Emote="Emote",EmoteBind="Emote Bind",
SuperJump="Super Jump",JumpPower="Jump Power",NoJumpCooldown="No Jump Cooldown",
DelayChanger="Delay Changer",DelayMs="Delay(ms)",NoSpread="No Spread",SpreadAmount="Spread Amount",RapidFire="Rapid Fire",RapidDelay="Rapid Delay(ms)",
InfRange="Infinite Range",InfMaxRange="Max Range",HitboxExp="Hitbox Expander",HitboxSize="Hitbox Size",
AutoAmmo="Auto Ammo",AutoAmmoAmount="Ammo Amount (1-1000)",
Utility="Utility",AntiTrip="Anti Trip",AntiStomp="Anti Stomp",CleanScripts="Clean Scripts",NoRecoil="No Recoil",AutoReload="Auto Reload",SmartAutoReload="Smart Auto Reload",SmartReloadDelay="Reload Delay",RemoveSlowdowns="Remove Slowdowns",InstantStand="Instant Stand",NoSit="No Sit",NoVoidKill="No Void Kill",AutoSort="Auto Sort",AutoSortNow="Sort Now",
DoubleTap="Double Tap",Spoofing="Spoofing",Headless="Headless",Korblox="Korblox",
Purchases="Purchases",BuyItem="Buy Item",AutoArmor="Auto Armor",ArmorAt="Armor At %",AutoBuy="Auto Buy",AutoBuyItems="Auto Buy Items",
PlayersSection="Players",Teleport="Teleport",TeleportEnable="Enable",TeleportMode="Mode",TeleportDist="Distance",TeleportSpeed="Speed",
ViewAim="View Aim Line",RagebotTag="Ragebot Target",Whitelisted="Whitelisted",TeleportTo="Teleport To",FollowT="Follow",
ConfigSection="Configs",ConfigName="Config Name...",Save="Save",Load="Load",Delete="Del",
Language="Language",Unload="Unload Script",PressKey="Press key...",Keybind="Keybind",Clear="Clear",Cancel="Cancel",OK="OK",BindKey="Bind",
ThemeColor="Theme Color",PanicInfo="F9 = Panic",UIToggleKey="UI Open Key",UISettings="UI Settings",UITransparency="BG Transparency",UIFont="UI Font",RainbowTheme="Rainbow",
NoWeapon="Unarmed",Follow="Follow",Orbit="Orbit",NoFiles="no file support",BindMode="Mode",
CatGuns="Guns",CatAmmo="Ammo",CatOther="Food/Armor/Tools",Start="Start",Exit="Exit"},
CN={TabAim="瞄准",TabVisuals="视觉",TabMisc="其他",TabPlayers="玩家",TabSettings="设置",
SilentAim="Hate 无声瞄准",HitPart="瞄准部位",UsePrediction="启用预判",PredX="预判X",PredY="预判Y",PredZ="预判Z",
AimAssist="辅助瞄准",AssistStyle="模式",Smoothing="平滑度",Sticky="粘性",AssistFOV="辅助FOV开关",AssistFOVSize="FOV大小",
SAFOV="无声FOV",SAFOVEnabled="SA FOV开",SAFOVVisible="SA FOV可见",SAFOVSize="SA FOV大小",SAFOVThickness="SA FOV粗细",SAFOVColor="SA FOV颜色",
ModeToggle="切换",ModeHold="按住",RageMode="Hate 狂暴模式",RageDelay="狂暴间隔",RageTracers="狂暴轨迹",RageImpacts="狂暴落点",WallCheck="墙体检查",RageInfRange="无限射程",RageColor="狂暴ESP颜色",
JujuSA="Juju 无声瞄准",JujuSticky="粘性",JujuHitChance="命中率",JujuMultipoint="多点命中",JujuAntiCurve="反曲线",JujuACVal="反曲线值",JujuAirHB="空中Hitbox",JujuBacktrack="回溯",JujuBTLife="回溯寿命",
Ragebot="狂暴机器人 (总开关)",SelectTargets="选择目标 (右键取消)",IncludeAimbot="包含瞄准辅助目标",AutoEquip="自动装备",AutoEquipWeapon="装备武器",AttachTarget="跟随/环绕目标",AttachMode="附加模式",StrafeSpeed="环绕速度",HOffset="水平偏移",VOffset="垂直偏移",TeleportBullets="子弹传送",ViewTarget="观战目标",AutoShoot="自动射击",AutoStomp="自动踩踏",TeleportBack="传送回原位",
TriggerBot="自动扳机",TriggerDelay="延迟",TriggerRadH="水平半径",TriggerRadV="垂直半径",TriggerJumpPred="跳跃预测",SpecificWeapons="特定武器",WeaponList="武器列表",
Resolver="目标解析器",ResolverRT="随机传送解析",ResolverNet="网络解析",RefreshRate="刷新率",
Desync="假同步",VelocityDesync="速度假同步",VelocityMode="速度模式",MultiplierVal="倍率",RandomVal="随机值",NetworkDesync="网络假同步",NetworkMode="网络模式",RandomTP="随机传送",TPHOff="水平偏移",TPVOff="垂直偏移",VoidSpam="虚空Spam",
DestroyCheaters="销毁作弊者",VoidKill="虚空击杀",
AntiAim="反瞄准",AnimationLag="动画延迟",AnimationLagVal="延迟值",AnimationSpam="动画Spam",AnimationSpamVal="动画",ClientPitch="客户端俯仰角",ClientPitchVal="俯仰值",FaceBackwards="背身",Spinbot="旋转机器人",SpinSpeed="旋转速度",
AntiAimViewer="反瞄准查看器",TeleportBullets2="子弹传送",
LPVisuals="本地玩家视觉",Trail="轨迹",TrailGradient="轨迹渐变",TrailColor="轨迹颜色",GradientColor="渐变颜色",ForcefieldBody="力场身体",ForcefieldBodyColor="身体颜色",ForcefieldHats="力场帽子",ForcefieldHatsColor="帽子颜色",MaterialTools="武器材质",MaterialValue="材质类型",MaterialColor="材质颜色",AccessoryAdder="帽子添加器",AccessoryID="帽子ID",AddAccessory="添加帽子",RemoveAccessory="移除全部",
ParticleAura="粒子光环",AuraValue="光环类型",AuraColor="光环颜色",
DesyncPos="脱同步模型",DesyncPosMat="材质",DesyncPosColor="颜色",DesyncPosHL="高亮",DesyncPosOL="描边颜色",
ESPAdv="ESP 集中设置",NameTagSize="名字大小",NameTagColor="名字颜色",WeaponESPSize="武器大小",WeaponESPColor="武器颜色",DistSize="距离大小",DistColor="距离颜色",BoxThick="方框粗细",
SkinChanger="皮肤更换",SkinWeapon="武器",SkinSelect="选择皮肤",FOVEnabled="FOV开",FOVVisible="FOV可见",FOVSize="FOV大小",FOVThickness="FOV粗细",FOVColor="FOV颜色",
LockLine="锁定线",LockLineColor="线颜色",LockLineThick="线粗细",TargetAim="目标锁定",KnockCheck="击倒检测",VisibleCheck="可见检测",
ESP="ESP",ESPBox="方框",ESPFill="填充",ESPChams="透视",ESPArmor="护甲条",Tracer="追踪线",WeaponESP="武器ESP",KeybindDisplay="按键显示",AntiRecord="防录屏",
KDPos="按键位置",KDSize="按键大小",KDColor="按键颜色",KDFont="按键字体",NameFont="名字字体",WeaponFont="武器字体",DistanceESP="距离ESP",WLColor="白名单颜色",BLColor2="黑名单颜色",BoxColor2="方框颜色",
ESPColors="ESP颜色",HealthBar="血量条",HealthText="血量数值",Skeleton="骨骼",
Effects="特效",LocalTracers="本地轨迹",TracerMode="模式",TracerTexture="贴图",TracerLife="寿命",TracerColor="颜色",
EnemyTracers="敌人轨迹",EnemyTracerMode="模式",EnemyTracerColor="颜色",EnemyTracerLife="寿命",Impacts="子弹落点",ImpactSize="落点大小",
OnHit="命中特效",HitSound="命中声音",HitSoundVolume="音量",DamageNumber="伤害数字",DamageMode="模式",DamageLife="寿命",
HitMarker="命中标记",HitMarkerMode="模式",HitChams="命中Chams",HitChamsMode="模式",OnlyLast="仅最后一次",FadeOut="淡出",ChamsLife="寿命",
HitSkeleton="命中骨骼",HitSkeletonOnly="仅最后",HitParticle="命中粒子",HitParticleValue="粒子",
World="世界",WorldMod="世界调节",Brightness="亮度",FogEnd="雾终点",TimeChanger="时间",Saturation="饱和度",Skybox="天空盒",AspectRatio="宽高比",AspectValue="宽高比值",
ViewHud="视野/界面",UnlockZoom="解锁视距",HideGunCrosshair="隐藏枪械准星",HideCursor="隐藏光标",ShowChat="显示聊天",
Crosshair="绘制准星",CrossFollow="跟随目标",CrossLoc="位置",CrossSmooth="平滑",CrossSpin="旋转",CrossSize="线长",CrossGap="间隙",
Watermark="水印",WaterText="文本",WaterPos="位置",WaterY="Y偏移",WaterSize="大小",
Notifications="通知",NotifStyle="通知风格",MoneyText="金钱文本",MoneyStyle="金钱风格",MoneyImage="金钱图片",
StatBars="自定义状态条",StatStyle="状态条风格",Hotbar="自定义快捷栏",HotbarStyle="快捷栏风格",
Movement="移动",CFrameSpeed="CFrame加速",SpeedValue="速度",CFrameFly="CFrame飞行",FlyValue="飞行速度",Noclip="穿墙",PreventFling="防飞踢",Emote="表情",EmoteBind="表情开关",
SuperJump="超级跳",JumpPower="跳跃力度",NoJumpCooldown="无跳冷却",
DelayChanger="冷却修改",DelayMs="延迟",NoSpread="无扩散",SpreadAmount="扩散量",RapidFire="快速射击",RapidDelay="间隔",
InfRange="无限射程",InfMaxRange="最大射程",HitboxExp="命中框",HitboxSize="大小",
AutoAmmo="自动弹药",AutoAmmoAmount="弹药数量(1-1000)",
Utility="实用",AntiTrip="防摔",AntiStomp="防处决",CleanScripts="清理脚本",NoRecoil="无后坐力",AutoReload="自动换弹",SmartAutoReload="智能换弹",SmartReloadDelay="换弹延迟",RemoveSlowdowns="移除减速",InstantStand="瞬间起身",NoSit="禁止坐下",NoVoidKill="防虚空击杀",AutoSort="自动排序",AutoSortNow="立即排序",
DoubleTap="双重射击",Spoofing="伪装",Headless="无头",Korblox="Korblox",
Purchases="购买",BuyItem="购买物品",AutoArmor="自动护甲",ArmorAt="护甲低于%",AutoBuy="自动购买",AutoBuyItems="自动购买物品",
PlayersSection="玩家",Teleport="传送",TeleportEnable="启用",TeleportMode="模式",TeleportDist="距离",TeleportSpeed="速度",
ViewAim="查看瞄准线",RagebotTag="Ragebot目标",Whitelisted="白名单",TeleportTo="传送",FollowT="跟随",
ConfigSection="存档",ConfigName="存档名...",Save="保存",Load="读取",Delete="删除",
Language="语言",Unload="退出脚本",PressKey="按下按键...",Keybind="按键",Clear="清除",Cancel="取消",OK="确定",BindKey="绑定按键",
ThemeColor="主题色",PanicInfo="F9=隐藏",UIToggleKey="呼出键",UISettings="界面设置",UITransparency="背景透明",UIFont="字体",RainbowTheme="彩虹",
NoWeapon="空手",Follow="跟随",Orbit="环绕",NoFiles="不支持文件",BindMode="模式",
CatGuns="枪械",CatAmmo="枪械子弹",CatOther="食物/护甲/工具",Start="启动",Exit="退出"},
}
Translations.EN.StickyAim="Sticky Aim";Translations.EN.StickyFire="Fire Mode";Translations.EN.StickySpectate="Spectate";Translations.EN.StickyStomp="Stomp Target";Translations.EN.StickyInvBullets="Invisible Bullets";Translations.EN.StickyTracer="Tracer";Translations.EN.StickyTracerMode="Tracer Mode";Translations.EN.StickyTracerColor="Tracer Color";Translations.EN.StickyFOV="FOV Box";Translations.EN.StickyFOVSize="FOV Size";Translations.EN.StickyFOVColor="FOV Color";Translations.EN.RapidFireV2="Rapid Fire v2";Translations.EN.RemoveShootAnim="Remove Shoot Animations";Translations.EN.ESPNames="Names";Translations.EN.ESPNameMode="Name Mode";Translations.EN.ESPOutline="Outline"
Translations.CN.StickyAim="吸附瞄准";Translations.CN.StickyFire="开火模式";Translations.CN.StickySpectate="观战";Translations.CN.StickyStomp="踩踏目标";Translations.CN.StickyInvBullets="隐形子弹";Translations.CN.StickyTracer="追踪线";Translations.CN.StickyTracerMode="追踪线模式";Translations.CN.StickyTracerColor="追踪线颜色";Translations.CN.StickyFOV="FOV框";Translations.CN.StickyFOVSize="FOV大小";Translations.CN.StickyFOVColor="FOV颜色";Translations.CN.RapidFireV2="快速射击v2";Translations.CN.RemoveShootAnim="移除射击动画";Translations.CN.ESPNames="显示名字";Translations.CN.ESPNameMode="名字模式";Translations.CN.ESPOutline="描边"
Translations.EN.Pqnd4Kick="Pqnd4 Kick";Translations.EN.Atmosphere="Atmosphere";Translations.EN.AtmosphereColor="Atmosphere Color";Translations.EN.AtmosphereDecay="Atmosphere Decay";Translations.EN.AtmosphereDensity="Atmosphere Density";Translations.EN.AtmosphereGlare="Atmosphere Glare";Translations.EN.AtmosphereHaze="Atmosphere Haze";Translations.EN.Exposure="Exposure";Translations.EN.ExposureValue="Exposure Value";Translations.EN.Saturation="Saturation";Translations.EN.StickyStrafe="Target Strafe";Translations.EN.StickyStrafeMode="Strafe Mode";Translations.EN.StickyStrafeSpeed="Strafe Speed";Translations.EN.StickyStrafeOffset="Z Offset";Translations.EN.StickySpectateStrafe="Spectate Strafe"
Translations.CN.Pqnd4Kick="Pqnd4 假踢";Translations.CN.Atmosphere="大气";Translations.CN.AtmosphereColor="大气颜色";Translations.CN.AtmosphereDecay="大气衰减";Translations.CN.AtmosphereDensity="大气密度";Translations.CN.AtmosphereGlare="大气眩光";Translations.CN.AtmosphereHaze="大气雾霾";Translations.CN.Exposure="曝光";Translations.CN.ExposureValue="曝光值";Translations.CN.Saturation="饱和度";Translations.CN.StickyStrafe="环绕目标";Translations.CN.StickyStrafeMode="环绕模式";Translations.CN.StickyStrafeSpeed="环绕速度";Translations.CN.StickyStrafeOffset="Z偏移";Translations.CN.StickySpectateStrafe="环绕观战"
-- // [新增] Aimbot / Aim Assist / Desync 翻译 //
Translations.EN.Aimbot="Aimbot";Translations.EN.AutoSelect="Auto select target";Translations.EN.AutoSelectDelay="Auto select delay (ms)";Translations.EN.AimSticky="Sticky";Translations.EN.AimHitPart="Hit part";Translations.EN.AimAirHitPart="Air hit part";Translations.EN.AimMaxDist="Max distance";Translations.EN.TargetBind="Target bind";Translations.EN.AimUseFOV="Use FOV (aimbot)";Translations.EN.AimFOVSize="Aimbot FOV size";Translations.EN.AimFOVVisible="Show aimbot FOV";Translations.EN.AimFOVThick="Aimbot FOV thickness";Translations.EN.AimFOVColor="Aimbot FOV color";Translations.EN.AimWallCheck="Ignore targets behind walls"
Translations.CN.Aimbot="自瞄 (Aimbot)";Translations.CN.AutoSelect="自动选择目标";Translations.CN.AutoSelectDelay="自动换目标延迟(ms)";Translations.CN.AimSticky="粘住目标";Translations.CN.AimHitPart="命中部位";Translations.CN.AimAirHitPart="空中命中部位";Translations.CN.AimMaxDist="最大距离";Translations.CN.TargetBind="锁定目标键";Translations.CN.AimUseFOV="启用FOV(自瞄)";Translations.CN.AimFOVSize="自瞄FOV大小";Translations.CN.AimFOVVisible="显示自瞄FOV";Translations.CN.AimFOVThick="自瞄FOV粗细";Translations.CN.AimFOVColor="自瞄FOV颜色";Translations.CN.AimWallCheck="隔墙不瞄"
Translations.EN.StickyFireDelay="Sticky fire delay (ms)";Translations.CN.StickyFireDelay="吸附射速(ms)"
Translations.EN.HideUserId="Hide user ID (bottom-right)";Translations.CN.HideUserId="隐藏右下角 ID/用户名"
Translations.EN.GridEmpty="Nothing to show here";Translations.EN.GridHintSingle="Left click = pick and close";Translations.EN.GridHintMulti="Left click = tick / untick, right click = clear, Esc = close";Translations.EN.CatAll="All known items";Translations.CN.CatAll="全部已知物品"
Translations.EN.RageDisableKnocked="Disable attach if target knocked";Translations.EN.RageShootDelay="Ragebot shoot delay (ms)";Translations.EN.RageMaxDist="Ragebot max distance"
Translations.EN.RagePacketShoot="Packet shoot (send damage to server)";Translations.EN.RageRequireResolver="Only shoot when resolver locks target";Translations.EN.RageSpeedLimit="Target speed limit (resolver gate)"
Translations.CN.RageDisableKnocked="目标被K时停止吸附";Translations.CN.RageShootDelay="Ragebot射速(ms)";Translations.CN.RageMaxDist="Ragebot最大距离"
Translations.CN.RagePacketShoot="包体射击(向服务器发送伤害)";Translations.CN.RageRequireResolver="仅解析到目标时开枪";Translations.CN.RageSpeedLimit="目标移速阈值(解析门控)"
Translations.CN.GridEmpty="这里没有可显示的内容";Translations.CN.GridHintSingle="左键点击即选择并关闭";Translations.CN.GridHintMulti="左键勾选/取消, 右键清空勾选, Esc 关闭";Translations.CN.CatAll="全部已知物品"
Translations.EN.AimAssist="Aim assist";Translations.EN.AssistStyle="Assist style";Translations.EN.SmoothStyle="Smoothing style";Translations.EN.HSmoothness="Horizontal smoothness";Translations.EN.VSmoothness="Vertical smoothness";Translations.EN.HPrediction="Horizontal prediction";Translations.EN.VPrediction="Vertical prediction";Translations.EN.JumpOffset="Jump offset";Translations.EN.Multipoint="Multipoint";Translations.EN.DontAimVertically="Don't aim vertically";Translations.EN.JumpPrediction="Jump prediction";Translations.EN.AAUseFOV="Use FOV (assist)";Translations.EN.AAFOVVisible="Show FOV";Translations.EN.AAFOVSize="Assist FOV size";Translations.EN.AAFOVThick="FOV thickness";Translations.EN.AAFOVColor="FOV color";Translations.EN.FallbackCamera="Camera fallback"
Translations.CN.AimAssist="瞄准辅助";Translations.CN.AssistStyle="辅助方式";Translations.CN.SmoothStyle="平滑风格";Translations.CN.HSmoothness="水平平滑度";Translations.CN.VSmoothness="垂直平滑度";Translations.CN.HPrediction="水平预测";Translations.CN.VPrediction="垂直预测";Translations.CN.JumpOffset="跳跃偏移";Translations.CN.Multipoint="多点命中";Translations.CN.DontAimVertically="不修正垂直";Translations.CN.JumpPrediction="跳跃预测";Translations.CN.AAUseFOV="启用FOV(辅助)";Translations.CN.AAFOVVisible="显示FOV";Translations.CN.AAFOVSize="辅助FOV大小";Translations.CN.AAFOVThick="FOV粗细";Translations.CN.AAFOVColor="FOV颜色";Translations.CN.FallbackCamera="相机回退";Translations.EN.AimTargetHelp="Target: auto-selects the closest player inside FOV";Translations.CN.AimTargetHelp="目标: 自动锁定 FOV 内最近的人";Translations.EN.AAFOVMouse="FOV follows mouse";Translations.CN.AAFOVMouse="FOV跟随鼠标光标";Translations.EN.AutoPrediction="Auto prediction (+ping)";Translations.CN.AutoPrediction="自动预测(叠加Ping)";Translations.EN.JumpPredictionVal="Jump prediction (ms)";Translations.CN.JumpPredictionVal="跳跃预测(ms)";Translations.EN.SmoothLockHint="Smoothness: 1 = hard lock, higher = smoother";Translations.EN.AimStatusOff="Aim assist is OFF";Translations.CN.AimStatusOff="瞄准辅助未开启";Translations.EN.AimStatusLocked="Target";Translations.CN.AimStatusLocked="已锁定";Translations.EN.AimStatusNone="No target";Translations.CN.AimStatusNone="未选到目标";Translations.EN.AimStatusFound="candidates";Translations.CN.AimStatusFound="候选";Translations.EN.AimStatusFov="FOV";Translations.CN.AimStatusFov="FOV"
Translations.EN.SortPlanName="Plan name";Translations.CN.SortPlanName="方案名称";Translations.EN.SortPlanSave="Save current order";Translations.CN.SortPlanSave="保存当前排序";Translations.EN.SortPlanPick="Select plan";Translations.CN.SortPlanPick="选择方案";Translations.EN.SortPlanApply="Apply plan";Translations.CN.SortPlanApply="应用方案";Translations.EN.SortPlanDel="Delete plan";Translations.CN.SortPlanDel="删除方案";Translations.EN.SortPlanNone="No saved plan";Translations.CN.SortPlanNone="暂无已保存方案"
Translations.EN.MoveOnly="Only while moving";Translations.EN.ColorBtn="Colors";Translations.EN.DesyncDepth="Desync depth";Translations.EN.EyeSize="Eye size";Translations.EN.NoBinds="No keybinds";Translations.EN.Desync="Desync";Translations.EN.ShowEye="Show eye";Translations.EN.RandomTP="Random teleport";Translations.EN.TPHOff="Teleport horizontal";Translations.EN.TPVOff="Teleport vertical";Translations.EN.KDPColor="Indicator color";Translations.EN.KeybindDisplay="Keybind indicator"
Translations.CN.MoveOnly="仅移动时生效";Translations.CN.ColorBtn="颜色";Translations.CN.DesyncDepth="假同步深度";Translations.CN.EyeSize="眼睛大小";Translations.CN.NoBinds="暂无按键绑定";Translations.CN.Desync="假同步 (Desync)";Translations.CN.ShowEye="显示眼睛(实时位置)";Translations.CN.RandomTP="随机传送";Translations.CN.TPHOff="水平随机范围";Translations.CN.TPVOff="垂直随机范围";Translations.CN.KDPColor="指示器颜色";Translations.CN.KeybindDisplay="按键绑定显示"
Translations.CN.EyeColor="眼睛颜色";Translations.CN.HitSoundValue="音效";Translations.CN.StatColors="状态条颜色";Translations.CN.CustomShoot="自定义开枪音效";Translations.CN.ShootSoundValue="开枪音效";Translations.CN.ShootVolume="开枪音量"
Translations.EN.None="None";Translations.EN.ModeToggle="Toggle";Translations.EN.ModeHold="Hold";Translations.CN.None="未绑定";Translations.EN.TabMisc="Misc";Translations.EN.TabPlayers="Players";Translations.EN.TabSettings="Settings"
function T(k) return (Translations[CurrentLang] and Translations[CurrentLang][k]) or Translations.EN[k] or k end
LangLabels={}
BindSuffixSet={}
function registerLang(o,k) table.insert(LangLabels,{obj=o,key=k}); o.Text=T(k)..(BindSuffixSet[o] and (" ("..T("BindKey")..")") or "") end
function refreshLanguage() for _,it in pairs(LangLabels) do pcall(function() it.obj.Text=T(it.key)..(BindSuffixSet[it.obj] and (" ("..T("BindKey")..")") or "") end) end end
ItemCN={revolver="左轮手枪",glock="格洛克",silencer="消音手枪",deagle="沙鹰",shotgun="霰弹枪",doublereloadsg="双管霰弹枪",tacticalshotgun="战术霰弹枪",drumshotgun="鼓式霰弹枪",["drum-shotgun"]="鼓式霰弹枪",["double-barrelsg"]="双管霰弹枪",smg="冲锋枪",rifle="步枪",ak47="AK47",ar="突击步枪",aug="AUG",drumgun="鼓枪",lmg="轻机枪",p90="P90",flintlock="燧发枪",knife="小刀",taser="电击枪",paintball="彩弹枪",flaregun="信号枪",snowball="雪球",sword="剑",bat="球棒",
revolverammo="左轮子弹",glockammo="格洛克子弹",silencerammo="消音手枪子弹",silencerarammo="消音步枪子弹",deagleammo="沙鹰子弹",shotgunammo="霰弹枪子弹",doublereloadsgammo="双管霰弹枪子弹",tacticalshotgunammo="战术霰弹枪子弹",["drum-shotgunammo"]="鼓式霰弹枪子弹",["double-barrelsgammo"]="双管霰弹枪子弹",smgammo="冲锋枪子弹",rifleammo="步枪子弹",ak47ammo="AK47子弹",arammo="突击步枪子弹",augammo="AUG子弹",drumgunammo="鼓枪子弹",lmgammo="轻机枪子弹",p90ammo="P90子弹",flamethrowerammo="火焰喷射器弹药",rpgammo="火箭筒弹药",grenadelauncherammo="榴弹发射器弹药",ammo="子弹",
mediumarmor="中护甲",higharmor="高护甲",["high-mediumarmor"]="高中护甲",firearmor="火焰护甲",antidotes="解毒剂",bandage="绷带",medkit="医疗包",
pizza="披萨",chicken="鸡肉",burger="汉堡",hamburger="汉堡包",cola="可乐",water="水",cranberry="蔓越莓",lettuce="生菜",taco="塔可",donut="甜甜圈",meat="肉",popcorn="爆米花",hotdog="热狗",damilk="牛奶",starbloxlatte="星布乐拿铁",
phone="手机",lockpick="开锁器",lockpicker="开锁器",key="钥匙",bag="背包",radio="对讲机",jammers="干扰器",c4="C4",detonator="起爆器",mine="地雷",
flashlight="手电筒",flashbang="闪光弹",grenade="手榴弹",grenadelauncher="榴弹发射器",pepperspray="胡椒喷雾",teargas="催泪瓦斯",
basketball="篮球",sledgehammer="大锤",pitchfork="干草叉",riotmask="防暴面具",surgeonmask="外科面具",paintballmask="彩弹面具",ninjamask="忍者面具",whip="鞭子",hairglue="发胶",pencil="铅笔",stopsign="停车牌",defaultmoveset="默认动作",foodscart="食物车",flowers="花",tele="传送"}
function itemDisplay(n) if CurrentLang=="CN" then return ItemCN[n] or n end return n end
function getWeaponDisplayName(n) if not n or n=="" then return T("NoWeapon") end return itemDisplay(n) end
function serializeValue(v,ind)
ind=ind or "   "
local t=typeof(v)
if t=="string" then return string.format("%q",v)
elseif t=="number" or t=="boolean" then return tostring(v)
elseif t=="Color3" then return string.format("Color3.fromRGB(%d,%d,%d)",math.floor(v.R*255+0.5),math.floor(v.G*255+0.5),math.floor(v.B*255+0.5))
elseif t=="Vector2" then return string.format("Vector2.new(%s,%s)",tostring(v.X),tostring(v.Y))
elseif t=="Vector3" then return string.format("Vector3.new(%s,%s,%s)",tostring(v.X),tostring(v.Y),tostring(v.Z))
elseif t=="table" then
local parts={}; local sub=ind.."   "
for k,val in pairs(v) do
local ks=type(k)=="number" and ("["..k.."]") or ("["..string.format("%q",tostring(k)).."]")
table.insert(parts,sub..ks.." = "..serializeValue(val,sub))
end
if #parts==0 then return "{}" end
return "{\n"..table.concat(parts,",\n").."\n"..ind.."}"
end
return "nil"
end
function serializeTable(t) return "return "..serializeValue(t,"") end
function deserialize(s) local fn=loadstring(s) if not fn then return nil end local ok,r=pcall(fn) return ok and r or nil end
function deepMerge(d,s) for k,v in pairs(s) do if type(v)=="table" and type(d[k])=="table" then deepMerge(d[k],v) else d[k]=v end end end
CONFIG_FOLDER="HateConfigs"
function filesAvailable() return type(writefile)=="function" and type(readfile)=="function" end
function saveConfigFile(n) if not filesAvailable() then return false end pcall(function() if not isfolder(CONFIG_FOLDER) then makefolder(CONFIG_FOLDER) end end) pcall(function() writefile(CONFIG_FOLDER.."/"..n..".config",serializeTable({Config=Config,Whitelist=Whitelist,Blacklist=Blacklist})) end) return true end
function loadConfigFile(n) if not filesAvailable() then return false end local ok,c=pcall(function() return readfile(CONFIG_FOLDER.."/"..n..".config") end) if not ok or not c then return false end local d=deserialize(c) if not d then return false end if d.Config then deepMerge(Config,d.Config) end for k,d2 in pairs(DEFAULTS) do if type(d2)=="table" and type(Config[k])=="table" then mergeDefaults(Config[k],d2) end end pcall(sanitizeAimConfig) Whitelist=d.Whitelist or {} Blacklist=d.Blacklist or {} return true end
function listConfigFiles() local names={} if not filesAvailable() then return names end pcall(function() if not isfolder(CONFIG_FOLDER) then makefolder(CONFIG_FOLDER) end end) local ok,files=pcall(function() return listfiles(CONFIG_FOLDER) end) if ok and files then for _,f in pairs(files) do local n=f:match("([^/\\]+)%.config$") if n then table.insert(names,n) end end end return names end
function deleteConfigFile(n) pcall(function() if delfile and isfile(CONFIG_FOLDER.."/"..n..".config") then delfile(CONFIG_FOLDER.."/"..n..".config") end end) end
function newSignal() local s={c={}} function s:Fire(...) for _,cb in ipairs(s.c) do task.spawn(cb,...) end end function s:Connect(cb) table.insert(s.c,cb) return {Disconnect=function() for i,v in ipairs(s.c) do if v==cb then table.remove(s.c,i) break end end end} end return s end
hitPlayer=newSignal()
newTargetSignal=newSignal()
local localBulletHit={}
function isPlayerKnockedOrKO(pl)
if not Config.Settings['Knock Check'] then return false end
return isCharKO(pl and pl.Character)
end
function isSelfKnocked()
return isCharKO(LocalPlayer.Character)
end
function canSeeTarget(part)
if not Config.Settings['Visible Check'] then return true end
if not part or not part.Parent then return false end
local ch=part.Parent
local hum=ch:FindFirstChildOfClass("Humanoid") if not hum then return false end
local origin=Camera.CFrame.Position
local dir=(part.Position-origin)
local rp=RaycastParams.new(); rp.FilterDescendantsInstances={LocalPlayer.Character,ch}; rp.FilterType=Enum.RaycastFilterType.Exclude
local res=Workspace:Raycast(origin,dir.Unit*dir.Magnitude,rp)
return res==nil or res.Instance:IsDescendantOf(ch)
end
function isPartVisible(part)
function isPartVisible(part)
local ok,res=pcall(function()
if not part or not part.Parent then return false end
local ch=part:FindFirstAncestorOfClass('Model') or part.Parent
local origin=Camera.CFrame.Position
local dir=part.Position-origin
local mag=dir.Magnitude
if mag<0.1 then return true end
local rp=RaycastParams.new()
local filter={}
if LocalPlayer.Character then table.insert(filter,LocalPlayer.Character) end
table.insert(filter,ch)
local ign=getIgnoredFolder()
if ign then table.insert(filter,ign) end
rp.FilterDescendantsInstances=filter
rp.FilterType=Enum.RaycastFilterType.Exclude
local hit=Workspace:Raycast(origin,dir.Unit*(mag*0.995),rp)
return hit==nil or hit.Instance:IsDescendantOf(ch)
end)
return ok and res==true or not ok
end
local best,bd=nil,math.huge
for _,n in ipairs({"Head","UpperTorso","HumanoidRootPart","LowerTorso","LeftUpperArm","RightUpperArm","LeftHand","RightHand","LeftUpperLeg","RightUpperLeg","LeftFoot","RightFoot"}) do
local p=ch:FindFirstChild(n)
if p then local pos=Camera:WorldToViewportPoint(p.Position) local d=(Vector2.new(pos.X,pos.Y)-Vector2.new(Camera.ViewportSize.X/2,Camera.ViewportSize.Y/2)).Magnitude if d<bd then bd=d best=p end end
end
return best
end
function isMouseInFOV(ch,fovCfg)
fovCfg=fovCfg or Config.FOV
if not fovCfg.Enabled then return true end
if not ch then return false end
local rp=ch:FindFirstChild("HumanoidRootPart") if not rp then return false end
local pos,on=Camera:WorldToViewportPoint(rp.Position) if not on then return false end
return (Vector2.new(pos.X,pos.Y)-Vector2.new(Camera.ViewportSize.X/2,Camera.ViewportSize.Y/2)).Magnitude<=(fovCfg.Size/2)
end
function getValidTargetPlayers()
local cand={}
for _,pl in pairs(Players:GetPlayers()) do
if pl~=LocalPlayer and pl.Character and pl.Character:FindFirstChild("HumanoidRootPart") then
if not isPlayerKnockedOrKO(pl) and not isWhitelisted(pl) then table.insert(cand,pl) end
end
end
local bl={} for _,p in ipairs(cand) do if isBlacklisted(p) then table.insert(bl,p) end end
if #bl>0 then return bl end
return cand
end
function findClosestTarget(hp,fovCfg)
hp=hp or 'Head'; fovCfg=fovCfg or Config.FOV
local best,bd=nil,math.huge
for _,pl in ipairs(getValidTargetPlayers()) do
local part=hp=='Closest Part' and getClosestBodyPart(pl.Character) or pl.Character:FindFirstChild(hp)
if part and canSeeTarget(part) and isMouseInFOV(pl.Character,fovCfg) then
local pos=Camera:WorldToViewportPoint(part.Position)
local d=(Vector2.new(pos.X,pos.Y)-Vector2.new(Camera.ViewportSize.X/2,Camera.ViewportSize.Y/2)).Magnitude
if d<bd then bd=d best=part end
end
end
return best
end
function getPredictedPosition(part,cfgT)
if not cfgT.UsePrediction then return part.Position end
local vel=part.AssemblyLinearVelocity or part.Velocity or Vector3.new(0,0,0)
local p=cfgT.Prediction
if type(p)=="table" then return part.Position+Vector3.new(vel.X*(p.X or 0.133),vel.Y*(p.Y or 0.133),vel.Z*(p.Z or 0.133)) end
if p==0 then p=0.1245 end
return part.Position+(vel*p)
end
function updateResolver(pl,tChar,hrp)
if not pl or not hrp then return nil end
local RS=Config['Resolver']
local st=resolverState[pl]
if not RS.Enabled then
if st then st.forcePos=nil st.lastPos=nil st.highest=0 end
return nil
end
if not st then st={lastRefresh=0,highest=0} resolverState[pl]=st end
local now=tick()
if now-st.lastRefresh<(RS.RefreshRate or 0.095) then return st.forcePos end
st.lastRefresh=now
if not st.lastPos then st.lastPos=hrp.Position st.highest=0 return st.forcePos end
local distance=hrp.Position-st.lastPos
local lastPosition=st.lastPos
st.lastPos=hrp.Position
local total=distance.Magnitude
-- // [修复] 公式对齐 juju: 之前少了 magnitude/(random/100) 这一除数, 算出来的回溯点几乎为 0, 所以"随机传送解析"看起来完全没效果 //
if RS.RandomTeleport and total>0 then
local hum=tChar and tChar:FindFirstChildOfClass('Humanoid')
local md=hum and hum.MoveDirection or Vector3.new()
local valid=distance.Unit*(st.lastMoveDir or md)
local validOffset=(valid.Magnitude>0) and (valid*distance) or distance
local magnitude=validOffset.Magnitude
if magnitude>st.highest then st.highest=magnitude end
-- // 防止一次传送抖动把 highest 拉爆, 之后永远回溯过头 //
if st.highest>60 then st.highest=60 end
local placeholder=math.max(st.highest*100,2)
local lo=math.max(math.floor(placeholder/8),1)
local hi=math.max(math.floor(placeholder),lo)
local divisor=math.random(lo,hi)/100
if divisor<=0 then divisor=0.01 end
local newp=hrp.Position-(validOffset*(magnitude/divisor))
st.forcePos=newp;st.lastForce=now
st.lastMoveDir=md
task.delay(0.03,function() if resolverState[pl]==st and st.forcePos==newp then st.forcePos=nil end end)
end
if RS.Network then
local sleeping=ghp(hrp,'NetworkIsSleeping')
if sleeping then st.lastSleep=now end
if st.lastSleep and now-st.lastSleep<0.3 then
st.forcePos=lastPosition;st.lastForce=now
task.delay(0.3,function() if resolverState[pl]==st and st.forcePos==lastPosition then st.forcePos=nil end end)
end
end
if total>=9e9 then st.forcePos=lastPosition st.lastMoveDir=nil st.highest=0 st.lastPos=hrp.Position return st.forcePos end
return st.forcePos
end
function resolverForcePos(pl)
local st=pl and resolverState[pl]
return st and st.forcePos or nil
end
function getStickyLockPart()
local pl=stickyTargetPlayer
if not pl then return nil end
local ch=pl.Character
if not ch or not ch.Parent then return nil end
if isWhitelisted(pl) or isPlayerKnockedOrKO(pl) then return nil end
local hum=ch:FindFirstChildOfClass("Humanoid") if not hum or hum.Health<=0 then return nil end
return Config['Sticky'].HitPart=='Closest Part' and getClosestBodyPart(ch) or ch:FindFirstChild(Config['Sticky'].HitPart)
end
function lockStickyTarget()
if isTyping() then return end
stickyLocked=false;stickyTargetPlayer=nil;currentTarget=nil;isLocking=false
if not Config['Sticky'].Enabled then return end
local ST=Config['Sticky']
local best,bd=nil,math.huge
local center=(ST.TracerMode=='HumanoidRootPart') and Vector2.new(Camera.ViewportSize.X/2,Camera.ViewportSize.Y/2) or UserInputService:GetMouseLocation()
for _,pl in ipairs(getValidTargetPlayers()) do
local ch=pl.Character
local part=ST.HitPart=='Closest Part' and getClosestBodyPart(ch) or ch:FindFirstChild(ST.HitPart)
if part then
local sp,on=Camera:WorldToViewportPoint(part.Position)
if on then
local d=(Vector2.new(sp.X,sp.Y)-center).Magnitude
if (not ST.FOVEnabled or d<=ST.FOVSize/2) and d<bd then bd=d best=pl end
end
end
end
if best then
stickyLocked=true;stickyTargetPlayer=best;isLocking=true
currentTarget=getStickyLockPart()
end
end
-- // [juju移植] Aimbot 替换 CamLock (核心逻辑见脚本尾部整合模块) //
fovCircle=Drawing.new("Circle");fovCircle.Visible=false;fovCircle.NumSides=60;fovCircle.Filled=false
lockLine=Drawing.new("Line");lockLine.Visible=false
stickyTracer=Drawing.new("Line");stickyTracer.Visible=false;stickyTracer.Thickness=1
stickyFov=Drawing.new("Circle");stickyFov.Visible=false;stickyFov.NumSides=60;stickyFov.Filled=false
function updateFOVCircle()
if Unloaded then fovCircle.Visible=false stickyFov.Visible=false return end
-- // [清理] 独立的"FOV"开关与 Aimbot 模块都已删除; fovCircle 只作为遗留画布保持隐藏 (见 updateAimFOV) //
if Config['Sticky'].Enabled and Config['Sticky'].FOVEnabled and not PanicMode and Started then
stickyFov.Visible=true;stickyFov.Radius=Config['Sticky'].FOVSize/2;stickyFov.Position=Vector2.new(Camera.ViewportSize.X/2,Camera.ViewportSize.Y/2);stickyFov.Thickness=1.5;stickyFov.Color=Config['Sticky'].FOVColor
else stickyFov.Visible=false end
end
function updateLockLine()
if Unloaded or PanicMode or not Started then lockLine.Visible=false return end
if not Config['Lock Line'].Enabled then lockLine.Visible=false return end
local t=nil
if currentTarget and currentTarget.Parent then t=currentTarget end
if t then
local pos,on=Camera:WorldToViewportPoint(t.Position)
if on then lockLine.Visible=true lockLine.From=Vector2.new(Camera.ViewportSize.X/2,Camera.ViewportSize.Y/2) lockLine.To=Vector2.new(pos.X,pos.Y) lockLine.Color=Config['Lock Line'].Color lockLine.Thickness=Config['Lock Line'].Thickness return end
end
lockLine.Visible=false
end
-- // TriggerBot 由脚本尾部整合模块重新定义 (juju 风格) //
grm=getrawmetatable(game)
oldIndex=grm.__index
oldNamecall=grm.__namecall
oldNewindex=grm.__newindex
setreadonly(grm,false)
grm.__index=function(self,key)
if infRangeActive and not checkcaller() and typeof(self)=="Instance" and type(key)=="string" then
local lk=string.lower(key)
if lk:find("range",1,true) or lk:find("dist",1,true) then
local ok,val=pcall(function() return oldIndex(self,key) end)
if ok and type(val)=="number" then return 9e9 end
end
end
if not Unloaded and Started and not checkcaller() and self==Mouse and key=="Hit" then
if Config.Ragebot.Enabled and Config.Ragebot.AutoShoot and ragebotAimPart and ragebotAimPart.Parent then
if ragebotFakePos then return CFrame.new(ragebotFakePos) end
local vel=ragebotAimPart.AssemblyLinearVelocity or Vector3.new(0,0,0)
return CFrame.new(ragebotAimPart.Position+vel*0.133)
end
if Config['Sticky'].Enabled and stickyLocked and not Config['Sticky'].AutoFire then
local part=currentTarget
if part and part.Parent then
local pl=Players:GetPlayerFromCharacter(part.Parent)
if pl and not isWhitelisted(pl) and not isPlayerKnockedOrKO(pl) then
return CFrame.new(part.Position)
end
end
end
end
return oldIndex(self,key)
end
grm.__newindex=function(self,key,value)
if not checkcaller() and self==Camera and key=="CFrame" and Config.Utility.NoRecoil then
local ok,cs=pcall(getcallingscript)
if ok and cs and cs.Name=="Framework" then return end
end
return oldNewindex(self,key,value)
end
grm.__namecall=function(self,...)
local args=table.pack(...)
local method=getnamecallmethod and getnamecallmethod() or nil
if not checkcaller() and method=="FireServer" and (self.Name==getMainEventName() or self.Name=='MainEvent' or self.Name=='MAINEVENT') then
if args[1]=='ShootGun' and Config['Double Tap'].Enabled then
local handle=args[2]
local toolName=(typeof(handle)=="Instance") and (handle.Parent and handle.Parent.Name) or nil
if toolName then
local ok=false
for _,w in ipairs(Config['Double Tap'].Weapons) do if w==toolName then ok=true break end end
if ok then
local tool=handle.Parent
local ammo=getToolAmmo(tool)
if not ammo or ammo.Value>=2 then
task.delay(0.05,function()
if Unloaded then return end
local hit=currentTarget and currentTarget.Parent and CFrame.new(currentTarget.Position) or args[4]
pcall(function() self:FireServer('ShootGun',handle,args[3],hit,args[5],args[6]) end)
end)
end
end
end
end
end
return oldNamecall(self,table.unpack(args,1,args.n))
end
setreadonly(grm,true)
local function isSpreadRange(min,max)
if type(min)~="number" or type(max)~="number" then return false end
local width=max-min
if width<=0 or width>2 then return false end
if math.abs(min+max)>0.001 then return false end
return true
end
originalRandom=math.random
oldRandom=hookfunction(math.random,function(...)
if Unloaded or checkcaller() then return oldRandom(...) end
if not Config.Spread.Enabled then return oldRandom(...) end
if Config.Spread.SpecificWeapons.Enabled then
local tool=LocalPlayer.Character and LocalPlayer.Character:FindFirstChildOfClass("Tool")
if not tool then return oldRandom(...) end
local found=false
for _,w in pairs(Config.Spread.SpecificWeapons.Weapons) do if tool.Name==w then found=true break end end
if not found then return oldRandom(...) end
end
local factor=Config.Spread.Amount/100
local a={...}
if #a==0 then
local v=oldRandom()
return 0.5+(v-0.5)*factor
elseif #a==2 and isSpreadRange(a[1],a[2]) then
return oldRandom(a[1],a[2])*factor
end
return oldRandom(...)
end)
function nameLooksLikeRange(n) local l=string.lower(n) return l:find("range",1,true)~=nil or l:find("dist",1,true)~=nil end
irState={tool=nil,lastScan=0,vals={},attrs={},lastMod=0}
function irScan(tool)
irState.vals={};irState.attrs={}
pcall(function()
local function visit(inst)
if inst:IsA("NumberValue") or inst:IsA("IntValue") then if nameLooksLikeRange(inst.Name) then table.insert(irState.vals,inst) end end
pcall(function() for an,av in pairs(inst:GetAttributes()) do if type(av)=="number" and nameLooksLikeRange(an) then table.insert(irState.attrs,{inst=inst,name=an}) end end end)
for _,c in ipairs(inst:GetChildren()) do visit(c) end
end
visit(tool)
end)
end
local function irPatchModules()
pcall(function()
local mods=(getloadedmodules and getloadedmodules()) or {}
for _,m in ipairs(mods) do
pcall(function()
local t=require(m)
if type(t)=="table" then
local function scan(tbl,depth)
if depth>4 then return end
for k,v in pairs(tbl) do
if type(k)=="string" and type(v)=="number" and nameLooksLikeRange(k) then tbl[k]=9e9 end
if type(v)=="table" then pcall(function() scan(v,depth+1) end) end
end
end
scan(t,1)
end
end)
end
end)
end
do
-- // [新] RAGEBOT 主循环 (juju.lol 式) //
ragebotViewTarget=nil
ragebotFakePos=nil
-- // [juju] Ragebot Desync position: 吸附结束时清除网络层欺骗 //
function rageDesyncClear()
if rageDesyncActive then
rageDesyncActive=false;rageDesyncBase=nil;rageDesyncTarget=nil
local ch=LocalPlayer.Character
local hrp=ch and ch:FindFirstChild('HumanoidRootPart')
if hrp then shp(hrp,'NetworkOrigin',nil) end
end
end
function rageFireShot(gun)
if not gun or not gun.Parent then return false end
-- // [juju] 不真实开枪: 直接向服务器发送 ShootGun 伤害包 (与 Sticky 自动开火相同) //
-- // 无本地枪口/子弹特效; 调用处有 0.09s 限速, 防止持续发包导致 ping 无休止上升 //
local ev=getMainEvent()
if not ev then return false end
local handle=gun:FindFirstChild('Handle')
if not handle then return false end
local origin=handle.Position
local aimPos=ragebotFakePos or ragebotAimPart.Position
local ok=pcall(function() ev:FireServer('ShootGun',handle,origin,aimPos,ragebotAimPart,Vector3.new(0,0,-1)) end)
return ok
end
-- // [juju] 停止自动射击后延迟 0.5s Deactivate 武器 (对应 juju 的 terminate/do_terminate) //
rageAutoFiring=false;rageAutoTerminate=0
function rageAutoStop()
if not rageAutoFiring then return end
rageAutoTerminate=rageAutoTerminate>0 and rageAutoTerminate or tick()
if tick()-rageAutoTerminate>0.5 then
local g=LocalPlayer.Character and LocalPlayer.Character:FindFirstChildOfClass('Tool')
if g then pcall(function() g:Deactivate() end) end
rageAutoFiring=false;rageAutoTerminate=0
end
end
function rageRestoreView()
if not ragebotViewTarget then return end
ragebotViewTarget=nil
local h=LocalPlayer.Character and LocalPlayer.Character:FindFirstChildOfClass('Humanoid')
if h then pcall(function() Camera.CameraSubject=h end) end
end
track(LocalPlayer.CharacterAdded:Connect(function() ragebotViewTarget=nil;rageDesyncActive=false;rageDesyncBase=nil;rageDesyncTarget=nil end))
-- // [新增] 统一的 RG 目标写入入口: 玩家列表的 RG 按钮 和 Ragebot 的"选择目标"弹窗 共用同一份状态 //
-- // 取消某个人的 RG 时, 观战/吸附/子弹传送/解析 等所有子功能会立刻对他停止, 相机也会交还给自己 //
function setRagebotTargets(newList)
	local before={}
	for _,u in ipairs(Config.Ragebot.Targets or {}) do before[u]=true end
	local after={}
	local clean={}
	for _,u in ipairs(newList or {}) do
		u=tonumber(u)
		if u and not after[u] then after[u]=true table.insert(clean,u) end
	end
	Config.Ragebot.Targets=clean
	for u,_ in pairs(before) do
		if not after[u] then
			local pl=Players:GetPlayerByUserId(u)
			if pl then
				resolverState[pl]=nil
				if ragebotTarget==pl then ragebotTarget=nil;ragebotAimPart=nil;ragebotFakePos=nil end
				if ragebotViewTarget==pl then rageRestoreView() end
				if stickyTargetPlayer==pl then
					stickyLocked=false;stickyTargetPlayer=nil;currentTarget=nil;isLocking=false
					pcall(function() stickyRestoreView() end)
				end
				if aimbotTargetPlayer==pl then
					aimbotTargetPlayer=nil;aimbotTargetPart=nil;aimAssistPart=nil;targetBindLocked=false
				end
			end
		end
	end
	pcall(function() if buildPlayerList then buildPlayerList() end end)
	pcall(refreshAllComponents)
	pcall(updateKeybindDisplay)
end
track(RunService.RenderStepped:Connect(function(dt)
if Unloaded or not Started then return end
local RB=Config.Ragebot
local ch=LocalPlayer.Character if not ch then rageRestoreView() return end
local hrp=ch:FindFirstChild('HumanoidRootPart') if not hrp then rageRestoreView() return end
local hum=ch:FindFirstChildOfClass('Humanoid')
if not hum or hum.Health<=0 or isSelfKnocked() then
rageAutoStop()
ragebotTarget=nil;ragebotAimPart=nil;ragebotFakePos=nil;rageRestoreView();rageDesyncClear()
return
end
if not (RB.Enabled and bindActive('Ragebot')) then
rageAutoStop()
ragebotTarget=nil;ragebotAimPart=nil;ragebotFakePos=nil;rageRestoreView();rageDesyncClear()
return
end
local candidates={}
for _,uid in ipairs(RB.Targets or {}) do
local pl=Players:GetPlayerByUserId(uid)
if pl and pl~=LocalPlayer and pl.Character and pl.Character:FindFirstChild('HumanoidRootPart') and not isWhitelisted(pl) and not isPlayerKnockedOrKO(pl) then table.insert(candidates,pl) end
end
if RB.IncludeAimbotTarget then
local at=aimbotTargetPlayer
if not at and currentTarget and currentTarget.Parent then at=Players:GetPlayerFromCharacter(currentTarget.Parent) end
if at and at~=LocalPlayer and not isWhitelisted(at) and not isPlayerKnockedOrKO(at) then
local dup=false for _,p in ipairs(candidates) do if p==at then dup=true break end end
if not dup then table.insert(candidates,at) end
end
end
if #candidates==0 then rageAutoStop() ragebotTarget=nil;ragebotAimPart=nil;ragebotFakePos=nil;rageRestoreView();rageDesyncClear() return end
local closest=nil;local bd=math.huge
for _,pl in ipairs(candidates) do
local d=(pl.Character.HumanoidRootPart.Position-hrp.Position).Magnitude
if d<bd then bd=d closest=pl end
end
if not closest then rageAutoStop() ragebotTarget=nil;ragebotAimPart=nil;ragebotFakePos=nil;rageRestoreView();rageDesyncClear() return end
ragebotTarget=closest
local tChar=closest.Character
local tHrp=tChar:FindFirstChild('HumanoidRootPart')
if not tHrp then rageAutoStop() ragebotTarget=nil;ragebotAimPart=nil;ragebotFakePos=nil;rageRestoreView();rageDesyncClear() return end
ragebotAimPart=tChar:FindFirstChild('Head') or tHrp
-- // [修复] 解析器以前只在"吸附瞄准"里跑, ragebot 从来没调用过, 也算出来的回溯点也没人用 -> 三个解析功能全是死的 //
ragebotFakePos=updateResolver(closest,tChar,tHrp)
local aimPos=ragebotFakePos or ragebotAimPart.Position
if RB.AutoEquip then
for _,wn in ipairs(RB.AutoEquipWeapons or {}) do
local tool=ch:FindFirstChild(wn) or LocalPlayer.Backpack:FindFirstChild(wn)
if tool and tool.Parent~=ch then tool.Parent=ch end
end
end
if RB.ViewTarget then
local th=tChar:FindFirstChildOfClass('Humanoid')
if th then
pcall(function() Camera.CameraSubject=th end)
ragebotViewTarget=closest
else rageRestoreView() end
else rageRestoreView() end
local tKnocked=isCharKO(tChar)
-- // [修复] 吸附不再限帧(每帧跟随), 并且向前预判对手速度, 见下面 anchor 计算 //
if RB.AttachToTarget and not (RB.DisableIfKnocked and tKnocked) then
-- // [修复] 客户端看到的对手位置本来就是延迟的, 直接 TP 到上一帧位置必然慢一步 //
-- // // 按对手速度向前预判一个心跳/ping 步长再吸附, 高速目标也能跟得上 //
local tv=tHrp.AssemblyLinearVelocity
if typeof(tv)~="Vector3" then tv=tHrp.Velocity or Vector3.new() end
local anchor=tHrp.Position+tv*math.max(dt*2,0.1)
local cf
if RB.AttachMode=='Random Teleport' then
cf=CFrame.new(anchor+Vector3.new(math.random(-RB.HOffset,RB.HOffset),math.random(-RB.VOffset,RB.VOffset),math.random(-RB.HOffset,RB.HOffset)))
else
rageStrafeAngle=rageStrafeAngle+math.clamp((RB.StrafeSpeed*15)*dt,0,360)
if rageStrafeAngle>360 then rageStrafeAngle=0 end
local base=anchor+Vector3.new(0,RB.VOffset or 10,0)
cf=CFrame.Angles(0,math.rad(rageStrafeAngle),0)*CFrame.new(0,0,-(RB.HOffset or 10))+base
end
if RB.DesyncPosition then
-- // [juju Target 区 Desync position] 服务器端位置保持在吸附前原位(网络层欺骗), 只有客户端视觉贴到目标 //
-- // // 配合 Desynced Position 视觉体可以看到服务器认为你在的位置 //
if not rageDesyncActive then rageDesyncBase=hrp.Position end
rageDesyncTarget=closest
rageDesyncActive=true
shp(hrp,'NetworkOrigin',CFrame.new(rageDesyncBase))
else
rageDesyncClear()
end
hrp.CFrame=cf
end
local gun=ch:FindFirstChildOfClass('Tool')
if gun and gun:FindFirstChild('Handle') and gun.Name~='[RPG]' then
if RB.AutoShoot then
local ammo=getToolAmmo(gun)
local canFire=((not ammo) or ammo.Value>0) and not tKnocked and not tChar:FindFirstChild('GRABBING_CONSTRAINT')
local forcefield=tChar:FindFirstChild('ForceField')
if canFire and forcefield and forcefield:FindFirstChild('On') then canFire=forcefield.On.Value==false end
if canFire then
local origin=gun.Handle.Position
local aimTarget=ragebotFakePos or ragebotAimPart.Position
local dir=aimTarget-origin
local mag=dir.Magnitude
local maxD=RB.InfiniteRange and 9e9 or (RB.MaxDistance or 500)
local blocked=false
if RB.WallCheck then
local rp=RaycastParams.new()
local filter={ch,tChar}
local ign=getIgnoredFolder()
if ign then table.insert(filter,ign) end
rp.FilterDescendantsInstances=filter
rp.FilterType=Enum.RaycastFilterType.Exclude
blocked=Workspace:Raycast(origin,dir.Unit*math.max(mag,0.001),rp)~=nil
end
if (not blocked) and mag<=maxD then
-- // [juju] 直接向服务器发伤害包, 不本地真开枪; 限速 0.09s 防止 ping 无休止上升 //
-- // 配合解析器: 目标不稳定(移速过快/假同步反瞄准)时预留射击, 解析到 (forcePos) 的瞬间立刻发出 //
local rSt=resolverState[closest]
local rUnstable=rSt and rSt.lastForce and (tick()-rSt.lastForce)<0.6
if (not rUnstable or ragebotFakePos~=nil) then
if tick()-lastRageShot>=0.09 then
lastRageShot=tick()
if rageFireShot(gun) then rageAutoFiring=true;rageAutoTerminate=0 end
end
end
else
rageAutoStop()
end
else
rageAutoStop()
end
else
rageAutoStop()
end
end
end))
stickyViewOn=false
function stickyRestoreView()
if not stickyViewOn then return end
stickyViewOn=false
local h=LocalPlayer.Character and LocalPlayer.Character:FindFirstChildOfClass('Humanoid')
if h then pcall(function() Camera.CameraSubject=h end) end
end
-- // [新] STICKY (free.txt 移植) //
track(RunService.Heartbeat:Connect(function()
if Unloaded or not Started then stickyTracer.Visible=false stickyRestoreView() return end
if not Config['Sticky'].Enabled or not stickyLocked or not stickyTargetPlayer then stickyTracer.Visible=false stickyRestoreView() return end
local ch=LocalPlayer.Character if not ch then return end
local pl=stickyTargetPlayer
local tCh=pl and pl.Character
if not tCh or not tCh.Parent then stickyLocked=false;stickyTargetPlayer=nil;currentTarget=nil;stickyTracer.Visible=false stickyRestoreView() return end
local isKO=isCharKO(tCh)
local isGrabbed=tCh:FindFirstChild('GRABBING_CONSTRAINT')~=nil
local ST=Config['Sticky']
local ev=getMainEvent()
if ST.StompTarget and isKO and not isGrabbed then
local ut=tCh:FindFirstChild('UpperTorso')
local lhrp=ch:FindFirstChild('HumanoidRootPart')
if ut and lhrp then lhrp.CFrame=CFrame.new(ut.Position+Vector3.new(0,3,0)) end
if ev then pcall(function() ev:FireServer('Stomp') end) end
stickyTracer.Visible=false stickyRestoreView()
return
end
local part=currentTarget or getStickyLockPart()
if not part or not part.Parent then stickyTracer.Visible=false stickyRestoreView() return end
currentTarget=part
updateResolver(pl,tCh,part)
if ST.Strafe then
local lhrp=ch:FindFirstChild('HumanoidRootPart')
local tRoot=tCh:FindFirstChild('HumanoidRootPart')
if lhrp and tRoot then
if ST.StrafeMode=='Orbit' then
local angle=tick()*ST.StrafeSpeed
local off=Vector3.new(math.cos(angle)*ST.StrafeXOffset,-0.1,math.sin(angle)*ST.StrafeXOffset)
lhrp.CFrame=CFrame.new(tRoot.Position+off,tRoot.Position)
else
local off=Vector3.new(math.random(-20,20),math.random(-10,10),math.random(-20,20))
lhrp.CFrame=CFrame.new(tRoot.Position+off)*CFrame.Angles(math.rad(math.random(0,360)),math.rad(math.random(0,360)),math.rad(math.random(0,360)))
end
end
end
-- // [修复] 观战"开了关不掉": 之前把 CameraSubject 设成对手的 Humanoid, 却拿它和对手的 Model 比较, //
-- // 两者永远不相等 -> 关闭后视角永远回不来. 现在用显式标记 stickyViewOn 来还原. //
local wantView=ST.Spectate or (ST.SpectateStrafe and ST.Strafe)
if wantView then
local th=nil
if ST.Spectate then th=tCh:FindFirstChildOfClass('Humanoid') or tCh:FindFirstChild('Head')
else th=tCh:FindFirstChild('Head') or tCh:FindFirstChildOfClass('Humanoid') end
if th then pcall(function() Camera.CameraSubject=th end) stickyViewOn=true end
elseif stickyViewOn then stickyRestoreView() end
if ST.Tracer then
local cpos,on=Camera:WorldToViewportPoint(part.Position)
local to=nil
if ST.TracerMode=='Mouse' then to=UserInputService:GetMouseLocation()
else local lhrp=ch:FindFirstChild('HumanoidRootPart') if lhrp then local s2,o2=Camera:WorldToViewportPoint(lhrp.Position) if o2 then to=Vector2.new(s2.X,s2.Y) end end end
if on and to then stickyTracer.Visible=true;stickyTracer.From=Vector2.new(cpos.X,cpos.Y);stickyTracer.To=to;stickyTracer.Color=ST.TracerColor else stickyTracer.Visible=false end
else stickyTracer.Visible=false end
local tool=ch:FindFirstChildOfClass('Tool')
local handle=tool and tool:FindFirstChild('Handle')
if ST.AutoFire and handle and tool and getToolAmmo(tool) and not isKO and not isGrabbed then
local ammoVal=getToolAmmo(tool)
-- // [修复] 和 ragebot 一样的老问题: 以前每个 Heartbeat 裸发一次 ShootGun (~60次/秒), //
-- // 打不中时服务器一直收包收尾不了 -> ping 无限上涨直到卡死. 这里加射击间隔限流. //
if (not ammoVal) or ammoVal.Value>0 then
if tick()-lastStickyShot>=math.max(ST.FireDelay or 0.12,0.03) then
lastStickyShot=tick()
local origin=handle.CFrame.Position
-- // [新增] 吸附瞄准也吃解析器的回溯点, 否则"随机传送解析/网络解析"对吸附完全无效 //
local aim=resolverForcePos(pl) or part.Position
if ST.InvisibleBullets then origin=origin-Vector3.new(0,10,0) aim=aim-Vector3.new(0,10,0) end
if ev then pcall(function() ev:FireServer('ShootGun',handle,origin,aim,part,Vector3.new(0,0,-1)) end) end
end
end
end
end))
-- // 假同步 //
-- // [合并] 假同步逻辑见脚本尾部整合模块 (free Desync + Velocity/Network/RandomTP) //
-- // 反瞄准 //
local spamAnims={Floss="rbxassetid://10714340543",Hype="rbxassetid://10714369624"}
track(RunService.Heartbeat:Connect(function(dt)
if Unloaded or not Started then return end
local AA=Config['Anti Aim']
local ch=LocalPlayer.Character if not ch then return end
local hrp=ch:FindFirstChild('HumanoidRootPart')
local head=ch:FindFirstChild('Head')
local hum=ch:FindFirstChildOfClass('Humanoid')
if AA.Spinbot and hrp and hum then
pcall(function() hum.AutoRotate=false spinAngle=spinAngle+(AA.SpinbotSpeed*7.2)*dt hrp.CFrame=CFrame.new(hrp.Position)*CFrame.Angles(0,math.rad(spinAngle),0) end)
end
if AA.FaceBackwards and hrp then
pcall(function() local cp=Camera.CFrame.Position local dir=hrp.Position-cp hrp.CFrame=CFrame.new(hrp.Position,hrp.Position+Vector3.new(dir.X,0,dir.Z)) end)
end
if AA.ClientPitch and head then
pcall(function()
local neck=head:FindFirstChild('Neck')
if neck then
if not origNeckC1 then origNeckC1=neck.C1 end
neck.C1=CFrame.new(0,0,0)*CFrame.Angles(math.rad(AA.ClientPitchValue),0,0)
end
end)
elseif not AA.ClientPitch and origNeckC1 and head then
pcall(function() local neck=head:FindFirstChild('Neck') if neck then neck.C1=origNeckC1 end end)
end
if AA.AnimationSpam and hum then
pcall(function()
if not animSpamTrack or animSpamId~=AA.AnimationSpamValue then
if animSpamTrack then pcall(function() animSpamTrack:Stop() end) end
local anim=Instance.new("Animation");anim.AnimationId=spamAnims[AA.AnimationSpamValue] or spamAnims.Floss
animSpamTrack=hum:LoadAnimation(anim);animSpamId=AA.AnimationSpamValue
animSpamTrack:Play()
end
if animSpamTrack and not animSpamTrack.IsPlaying then animSpamTrack:Play() end
end)
elseif animSpamTrack then
pcall(function() animSpamTrack:Stop() end) animSpamTrack=nil;animSpamId=nil
end
if AA.AnimationLag and hum then
pcall(function()
local now=tick()
local cycle=0.3
local onFrac=AA.AnimationLagValue/100
local ph=(now%cycle)/cycle
animLagFreeze=ph<onFrac
for _,tr in ipairs(hum:GetPlayingAnimationTracks()) do
if animLagFreeze then tr.TimePosition=0.01 end
end
end)
end
end))
-- // [修复] 粒子光环 (Rate>0, 可开关) //
local function updateVisualsContinuous()
local ch=LocalPlayer.Character if not ch then return end
local L=Config['Local Player Visuals']
if not L.MaterialTools then return end
local mat=Enum.Material[L.MaterialToolsValue] or Enum.Material.ForceField
for _,p in pairs(ch:GetChildren()) do
if p:IsA('Tool') then
for _,d in pairs(p:GetDescendants()) do
if d:IsA('MeshPart') or d:IsA('Part') then d.Material=mat; if d:IsA('MeshPart') then d.TextureID='' end; d.Color=L.MaterialToolsColor end
end
end
end
end
-- // 脱同步模型 //
local function buildDesyncModel(ch)
if desyncModel then pcall(function() desyncModel:Destroy() end) desyncModel=nil end
pcall(function()
ch.Archivable=true
desyncModel=ch:Clone()
ch.Archivable=false
for _,p in pairs(desyncModel:GetChildren()) do
if p:IsA('MeshPart') or p:IsA('Part') then
p.CanCollide=false;p.Anchored=true
p.Material=Enum.Material[Config['Desynced Position'].Value] or Enum.Material.ForceField
p.Color=Config['Desynced Position'].Color
p.Transparency=0.5
if p.Name=='Head' then local d=p:FindFirstChild('face') if d then d:Destroy() end end
else p:Destroy() end
end
if Config['Desynced Position'].Highlight then
local hl=Instance.new('Highlight');hl.Adornee=desyncModel;hl.FillColor=Config['Desynced Position'].Color;hl.FillTransparency=0.8;hl.OutlineColor=Config['Desynced Position'].OutlineColor;hl.Parent=desyncModel
end
desyncModel.Name='\0'
desyncModel.Parent=Workspace
end)
end
track(RunService.RenderStepped:Connect(function()
if Unloaded then if desyncModel then desyncModel:Destroy() desyncModel=nil end return end
local DP=Config['Desynced Position']
local ch=LocalPlayer.Character
if DP.Enabled and ch and ch:FindFirstChild('HumanoidRootPart') then
if not desyncModel then buildDesyncModel(ch) end
if desyncModel and tick()-desyncModelLast>0.2 then
desyncModelLast=tick()
local rageHrp=ch:FindFirstChild('HumanoidRootPart')
local rageShow=rageDesyncActive and rageDesyncBase and rageHrp and (rageDesyncBase-rageHrp.Position).Magnitude>3.5
for _,p in pairs(ch:GetChildren()) do
local m=desyncModel:FindFirstChild(p.Name)
if m and (p:IsA('Part') or p:IsA('MeshPart')) then
if rageShow then
m.CFrame=CFrame.new(p.Position+(rageDesyncBase-rageHrp.Position))*(p.CFrame-p.Position)
elseif not desyncActiveThisFrame then
m.CFrame=p.CFrame
end
end
end
end
else
if desyncModel then pcall(function() desyncModel:Destroy() end) desyncModel=nil end
end
end))
track(LocalPlayer.CharacterAdded:Connect(function() desyncModel=nil end))
track(LocalPlayer.CharacterAdded:Connect(function(ch)
task.wait(0.8)
if Unloaded then return end
if not Config['Local Player Visuals'].AccessoryAdder then return end
for id,_ in pairs(accTemplates) do
task.wait(0.15)
equipAccessory(id)
end
end))
function applyTrail()
if trailObj then pcall(function() trailObj:Destroy() end) trailObj=nil end
local ch=LocalPlayer.Character; local hrp=ch and ch:FindFirstChild('HumanoidRootPart')
if not hrp then return end
local L=Config['Local Player Visuals']
if L.Trail then
local a0=Instance.new("Attachment");a0.Name='TrailA0';a0.Position=Vector3.new(0,0.5,0);a0.Parent=hrp
local a1=Instance.new("Attachment");a1.Name='TrailA1';a1.Position=Vector3.new(0,-0.5,0);a1.Parent=hrp
local t=Instance.new("Trail");t.Attachment0=a0;t.Attachment1=a1
t.Color=ColorSequence.new(L.TrailColor,L.TrailGradient and L.GradientColor or L.TrailColor)
t.Lifetime=0.5;t.LightEmission=1;t.Parent=hrp
trailObj=t
end
end
matToolOrig={}
local function applyMatToTool(tool,enabled)
pcall(function()
if not tool or not tool:IsA('Tool') then return end
local handle=tool:FindFirstChild('Handle')
if not handle or not handle:IsA('BasePart') then return end
local L=Config['Local Player Visuals']
if not matToolOrig[tool] then
local def=tool:FindFirstChild('Default')
matToolOrig[tool]={
hTex=handle:IsA('MeshPart') and handle.TextureID or nil,
hMat=handle.Material,hCol=handle.Color,
dTex=def and def:IsA('MeshPart') and def.TextureID or nil,
dMat=def and def:IsA('BasePart') and def.Material or nil,
dCol=def and def:IsA('BasePart') and def.Color or nil}
end
local o=matToolOrig[tool]
local mat=enabled and (Enum.Material[L.MaterialToolsValue] or Enum.Material.ForceField) or (o.hMat or Enum.Material.Plastic)
local col=enabled and L.MaterialToolsColor or (o.hCol or Color3.new(1,1,1))
handle.Material=mat;handle.Color=col
if handle:IsA('MeshPart') then handle.TextureID=enabled and '' or (o.hTex or '') end
local def=tool:FindFirstChild('Default')
if def and def:IsA('BasePart') then
def.Material=mat;def.Color=col
if def:IsA('MeshPart') then def.TextureID=enabled and '' or (o.dTex or '') end
local first=def:GetChildren()[1]
if first and first:IsA('BasePart') then first.Material=mat;first.Color=col end
end
end)
end
function applyMaterialTools()
local ch=LocalPlayer.Character
local L=Config['Local Player Visuals']
local function each(fn)
if ch then for _,t in pairs(ch:GetChildren()) do if t:IsA('Tool') then fn(t) end end end
for _,t in pairs(LocalPlayer.Backpack:GetChildren()) do if t:IsA('Tool') then fn(t) end end
end
each(function(t) applyMatToTool(t,L.MaterialTools) end)
end
track(LocalPlayer.CharacterAdded:Connect(function(ch)
task.wait(0.6)
if Unloaded then return end
if not Config['Local Player Visuals'].MaterialTools then return end
for _,t in pairs(ch:GetChildren()) do if t:IsA('Tool') then task.wait(0.1) applyMatToTool(t,true) end end
end))
accTemplates={}
function equipAccessory(id)
pcall(function()
local tpl=accTemplates[id]
if not tpl then return end
local ch=LocalPlayer.Character
local hum=ch and ch:FindFirstChildOfClass('Humanoid')
local head=ch and ch:FindFirstChild('Head')
if not hum or not head then return end
for _,a in pairs(addedAccessories) do if a.Name==tostring(id) then pcall(function() a:Destroy() end) end end
local acc=tpl:Clone()
acc.Name=tostring(id)
hum:AddAccessory(acc)
local h=acc:FindFirstChild('Handle')
if h then
h.CanCollide=false
local at=h:FindFirstChildOfClass('Attachment')
local w=Instance.new('Weld');w.Name='HateAccWeld'
w.Part0=h;w.Part1=head
w.C0=at and at.CFrame or CFrame.new(0,0,0)
w.C1=CFrame.new(0,0.6,0)
w.Parent=h
end
table.insert(addedAccessories,acc)
end)
end
function addAccessory(id)
pcall(function()
id=tonumber(id)
if not id then return end
if not accTemplates[id] then
local ok,asset=pcall(function() return InsertService:LoadLocalAsset("rbxassetid://"..id) end)
if not ok or not asset then return end
accTemplates[id]=asset
end
if not Config['Local Player Visuals'].AccessoryAdder then Config['Local Player Visuals'].AccessoryAdder=true end
equipAccessory(id)
end)
end
function pqndCreateTool()
if pqndTool then pqndTool:Destroy() end
pqndTool=Instance.new("Tool");pqndTool.RequiresHandle=false;pqndTool.Name="[Kick]"
local anim=Instance.new("Animation");anim.AnimationId="rbxassetid://2788306916"
pqndTool.Activated:Connect(function()
pqndTest=true
local chr=LocalPlayer.Character or LocalPlayer.CharacterAdded:Wait()
local hum=chr:FindFirstChild("Humanoid")
if hum then local at=hum:LoadAnimation(anim) at:AdjustSpeed(3.4) at:Play() end
task.wait(0.6)
local boom=LocalPlayer.Backpack:FindFirstChild("[Boombox]")
local ev=getMainEvent()
if boom and ev then
boom.Parent=LocalPlayer.Character
ev:FireServer("Boombox",tonumber(Config['Pqnd4 Kick'].SoundId))
boom.RequiresHandle=false
boom.Parent=LocalPlayer.Backpack
task.wait(1)
ev:FireServer("BoomboxStop")
else
local snd=Instance.new("Sound",Workspace);snd.SoundId="rbxassetid://"..Config['Pqnd4 Kick'].SoundId;snd:Play();task.wait(1);snd:Stop()
end
wait(1.4);pqndTest=false
end)
pqndTool.Parent=LocalPlayer:WaitForChild("Backpack")
end
function pqndRemoveTool()
local t=LocalPlayer.Backpack:FindFirstChild("[Kick]") or (LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("[Kick]"))
if t then t:Destroy() end
end
track(RunService.Heartbeat:Connect(function()
if not pqndTest then return end
local chr=LocalPlayer.Character if not chr then return end
local hrp=chr:FindFirstChild("HumanoidRootPart") if not hrp then return end
local old=hrp.Velocity
hrp.Velocity=Vector3.new(hrp.CFrame.LookVector.X*800,800,hrp.CFrame.LookVector.Z*800)
RunService.RenderStepped:Wait()
hrp.Velocity=old
end))
function removeAllAccessories()
for _,a in pairs(addedAccessories) do pcall(function() a:Destroy() end) end
addedAccessories={}
end
function hookJujuToolFX(tool)
track(tool.Activated:Connect(function()
if Unloaded or not Started then return end
local target=currentTarget
if Config.Ragebot.TeleportBullets and target and target.Parent then
pcall(function()
local rh=LocalPlayer.Character and LocalPlayer.Character:FindFirstChild('RightHand')
if rh then
local old=tool.Grip
local newGrip=(rh.CFrame*CFrame.new(0,-1,0,1,0,0,0,0,1,0,-1,0)):ToObjectSpace(CFrame.new(target.Position)):Inverse()
tool.Parent=LocalPlayer.Backpack; rh.Anchored=false; tool.Grip=newGrip; rh.Anchored=true; tool.Parent=LocalPlayer.Character
RunService.RenderStepped:Wait()
tool.Parent=LocalPlayer.Backpack; rh.Anchored=false; tool.Grip=old; tool.Parent=LocalPlayer.Character
end
end)
end
if Config['Anti Aim Viewer'].Enabled and target and target.Parent then
pcall(function()
local ev=getMainEvent()
if ev then ev:FireServer(GameCfg.arg,target.Position) end
end)
end
end))
end
function applyRemoveSlowdowns()
if slowConn then pcall(function() slowConn:Disconnect() end) slowConn=nil end
local ch=LocalPlayer.Character; local hum=ch and ch:FindFirstChildOfClass('Humanoid')
if not hum then return end
if Config.Utility.RemoveSlowdowns then
if hum.WalkSpeed<16 then hum.WalkSpeed=16 end
slowConn=hum:GetPropertyChangedSignal('WalkSpeed'):Connect(function() if hum.WalkSpeed<16 then hum.WalkSpeed=16 end end)
end
end
function applyInstantStand()
if instantStandConn then pcall(function() instantStandConn:Disconnect() end) instantStandConn=nil end
local ch=LocalPlayer.Character; local hum=ch and ch:FindFirstChildOfClass('Humanoid')
if not hum then return end
if Config.Utility.InstantStand then
hum:SetStateEnabled(Enum.HumanoidStateType.FallingDown,false)
instantStandConn=hum.StateChanged:Connect(function(_,ns) if ns==Enum.HumanoidStateType.FallingDown then hum:ChangeState(Enum.HumanoidStateType.GettingUp) end end)
end
end
function applyNoSit()
if sitConn then pcall(function() sitConn:Disconnect() end) sitConn=nil end
local ch=LocalPlayer.Character; local hum=ch and ch:FindFirstChildOfClass('Humanoid')
if not hum then return end
if Config.Utility.NoSit then
hum:SetStateEnabled(Enum.HumanoidStateType.Seated,false)
sitConn=hum:GetPropertyChangedSignal('Sit'):Connect(function() if hum.Sit then task.defer(function() hum.Sit=false end) end end)
end
end
function applyNoVoidKill() pcall(function() Workspace.FallenPartsDestroyHeight=Config.Utility.NoVoidKill and -9e9 or -500 end) end
function doAutoSort()
pcall(function()
local bp=LocalPlayer.Backpack
if not bp then return end
local slots=Config.Utility.AutoSortSlots or {}
local children=bp:GetChildren()
local done={}
for i=1,#children do
pcall(function() children[i].Parent=LocalPlayer end)
end
for i=1,9 do
local f=slots[i]
if not f or f=='' then continue end
for j=1,#children do
local c=children[j]
if c and c.Parent==LocalPlayer and not done[c.Name] and c.Name:lower():find(f:lower(),1,true) then
pcall(function() c.Parent=bp end)
done[c.Name]=true
end
end
end
for j=1,#children do
local c=children[j]
if c and c.Parent==LocalPlayer and not done[c.Name] then
pcall(function() c.Parent=bp end)
end
end
end)
end
-- // [juju] 实时监控: 背包物品变化 / 重生后若开着自动排序就立刻重排 //
task.spawn(function()
local sortLock=false
local function sortSoon()
if sortLock then return end
sortLock=true
task.wait(0.35)
sortLock=false
if Unloaded then return end
if not Config.Utility.AutoSort then return end
doAutoSort()
end
track(LocalPlayer.Backpack.ChildAdded:Connect(function() sortSoon() end))
track(LocalPlayer.Backpack.ChildRemoving:Connect(function() sortSoon() end))
track(LocalPlayer.CharacterAdded:Connect(function()
task.wait(1)
if Unloaded then return end
if Config.Utility.AutoSort then doAutoSort() end
end))
end)
local SkinModules=ReplicatedStorage:FindFirstChild('SkinModules')
local SkinData=nil;local AppliedSkins={}
local function LoadSkinData()
if SkinData then return SkinData end
local function looksLikeSkins(t,depth)
if not t or type(t)~='table' or depth>2 then return false end
local n=0
for k,v in pairs(t) do
if type(k)=='string' and k:find('%[') and k:find('%]') and (type(v)=='table' or type(v)=='string') then n=n+1 end
end
return n>=2
end
local function tryModule(ms)
if not ms or not ms:IsA('ModuleScript') then return nil end
local ok,res=pcall(function() return require(ms:Clone()) end)
if not ok or type(res)~='table' or next(res)==nil then return nil end
if looksLikeSkins(res,1) then return res end
for k,v in pairs(res) do
if type(k)=='string' and type(v)=='table' and (k:lower():find('skin') or k:lower():find('weapon') or k:lower():find('gun')) and looksLikeSkins(v,2) then return v end
end
return nil
end
local merged={}
local function merge(t) for k,v in pairs(t) do merged[k]=v end end
local function scanRoot(root)
if not root then return end
for _,ms in ipairs(root:GetDescendants()) do
if ms:IsA('ModuleScript') and ms.Name:lower():find('skin') then
local r=tryModule(ms)
if r then merge(r) return end
end
end
end
-- // [修复] 皮肤数据源兜底: SkinModules 模块 -> ReplicatedStorage/StarterPack/StarterPlayer 名称含 skin 的模块 -> 全模块内容扫描(武器名[xx]为键) //
local rm=ReplicatedStorage:FindFirstChild('SkinModules')
if rm and rm:IsA('ModuleScript') then local r=tryModule(rm) if r then merge(r) end end
if next(merged)==nil then scanRoot(ReplicatedStorage) end
if next(merged)==nil then scanRoot(game:GetService('StarterPack')) end
if next(merged)==nil then scanRoot(game:GetService('StarterPlayer')) end
if next(merged)==nil then
for _,ms in ipairs(ReplicatedStorage:GetDescendants()) do
if ms:IsA('ModuleScript') then
local r=tryModule(ms)
if r then merge(r) break end
end
end
end
SkinData=next(merged) and merged or nil
return SkinData
end
local function skinDataFor(data,weaponName)
if not data or not weaponName then return nil end
local ws=data[weaponName]
if ws then return ws end
local m=weaponName:match('%[(.-)%]')
if m and data[m] then return data[m] end
local lk=weaponName:lower()
for k2,v2 in pairs(data) do
if type(k2)=='string' and k2:lower()==lk then return v2 end
end
return nil
end
GetSkinList=function(weaponName)
local list={'None'}
local data=LoadSkinData() if not data then return list end
local ws=skinDataFor(data,weaponName)
if ws then for name in pairs(ws) do table.insert(list,name) end table.sort(list) end
return list
end
RemoveSkinFromTool=function(tool)
local rec=AppliedSkins[tool]
if not rec then return end
for part,o in pairs(rec.Parts or {}) do
pcall(function()
if part and part.Parent then
part.TextureID=o.tex
part.Transparency=o.trans
end
end)
end
if rec.Sound and rec.OrigSound then pcall(function() rec.Sound.SoundId=rec.OrigSound end) end
AppliedSkins[tool]=nil
end
ApplySkinToTool=function(tool,skinName)
if not tool then return end
-- // [修复] 收集所有 BasePart (刀 Handle 是普通 Part, 只收 MeshPart 会导致 0 候选而更换失败) //
local candidates={}
local handle=tool:FindFirstChild('Handle')
if handle and handle:IsA('BasePart') then table.insert(candidates,handle) end
local def=tool:FindFirstChild('Default')
if def and def:IsA('BasePart') then table.insert(candidates,def) end
for _,d in pairs(tool:GetDescendants()) do
if d:IsA('BasePart') and not table.find(candidates,d) then table.insert(candidates,d) end
end
if #candidates==0 then return end
if AppliedSkins[tool] and AppliedSkins[tool].SkinName==skinName then return end
RemoveSkinFromTool(tool)
local rec={SkinName=skinName,Parts={}}
for _,d in pairs(tool:GetDescendants()) do if d:IsA('Sound') and (d.Name=='Shoot' or d.Name=='ShootSound') then rec.Sound=d rec.OrigSound=d.SoundId break end end
for _,m in ipairs(candidates) do rec.Parts[m]={tex=m.TextureID,trans=m.Transparency} end
AppliedSkins[tool]=rec
local data=LoadSkinData()
if data then
-- // [juju] 键兜底: 全名 -> [括号] 名 -> 大小写不敏感 //
local ws=skinDataFor(data,tool.Name)
if ws then
local inf=ws[skinName] or (next(ws) and ws[next(ws)])
if type(inf)=='string' then inf={TextureID=inf} end
if inf and type(inf.TextureID)=='string' and inf.TextureID~='' then
for _,m in ipairs(candidates) do pcall(function() m.TextureID=inf.TextureID m.Transparency=0 end) end
end
end
end
end
local function ProcessToolForSkin(tool)
if not Config['Skin Changer'].Enabled then return end
local skin=Config['Skin Changer'].Skins[tool.Name]
if skin and skin~='' and skin~='None' then ApplySkinToTool(tool,skin) end
end
local function hookSkinChar(ch)
if not ch then return end
local function watchTool(t)
task.wait(0.1)
ProcessToolForSkin(t)
local conn=t:GetPropertyChangedSignal('Parent'):Connect(function()
if Unloaded then conn:Disconnect() return end
if t.Parent==ch then
task.wait(0.1)
ProcessToolForSkin(t)
end
end)
end
for _,c in pairs(ch:GetChildren()) do if c:IsA('Tool') then watchTool(c) end end
track(ch.ChildAdded:Connect(function(c) if c:IsA('Tool') then watchTool(c) end end))
end
if LocalPlayer.Character then hookSkinChar(LocalPlayer.Character) end
track(LocalPlayer.CharacterAdded:Connect(function(ch) task.wait(0.5) hookSkinChar(ch) end))
end
function CleanToolScripts(tool) if not tool or not Config.Utility.CleanScripts then return end for _,desc in pairs(tool:GetDescendants()) do if desc:IsA("LocalScript") then desc:Destroy() end end end
function WatchCharacterForScripts(ch)
if not ch then return end
for _,child in pairs(ch:GetChildren()) do if child:IsA("Tool") then CleanToolScripts(child) end end
track(ch.ChildAdded:Connect(function(child) if child:IsA("Tool") then task.wait(0.1) CleanToolScripts(child) hookJujuToolFX(child) end end))
end
SavedCFrame=Camera.CFrame;RestorePending=false
function QueueRestore()
if RestorePending then return end
RestorePending=true
task.defer(function() if RestorePending and Config.Utility.NoRecoil then Camera.CFrame=SavedCFrame end RestorePending=false end)
end
track(RunService.RenderStepped:Connect(function() if not RestorePending then SavedCFrame=Camera.CFrame end end))
do local recoilHooked=false
local function tryHookRecoil()
if recoilHooked then return true end
local e=getMainEvent()
if e then track(e.OnClientEvent:Connect(function(p) if p=="ShootingRecoil" then QueueRestore() end end)) recoilHooked=true return true end
return false
end
task.spawn(function() for _=1,60 do if Unloaded then return end if tryHookRecoil() then return end task.wait(0.5) end end)
end
function SetupAntiStomp(Character)
if not Character then return end
local be=Character:FindFirstChild(GameCfg.folderName) or Character:WaitForChild(GameCfg.folderName,10)
if not be then return end
local kn
local knNames={GameCfg.knocked}
if GameCfg.knocked~='K.O' then table.insert(knNames,'K.O') end
if GameCfg.knocked~='Knocked' then table.insert(knNames,'Knocked') end
for _,n in ipairs(knNames) do kn=be:FindFirstChild(n) if kn then break end end
if not kn then return end
track(kn:GetPropertyChangedSignal("Value"):Connect(function()
if Config.Utility.AntiStomp and kn.Value==true then
local hum=Character:FindFirstChildOfClass("Humanoid")
if hum then hum.Health=0 end
end
end))
end
function SetupUtility(Character)
if not Character then return end
local Humanoid=Character:WaitForChild("Humanoid",5) if not Humanoid then return end
track(Humanoid.StateChanged:Connect(function(_,ns)
if Config.Utility.AntiTrip then if ns==Enum.HumanoidStateType.FallingDown or ns==Enum.HumanoidStateType.Ragdoll then Humanoid:ChangeState(Enum.HumanoidStateType.GettingUp) end end
end))
SetupAntiStomp(Character)
applyRemoveSlowdowns();applyInstantStand();applyNoSit()
end
function SetupNoJumpCooldown(Character)
if not Character then return end
local Humanoid=Character:FindFirstChildOfClass("Humanoid") or Character:WaitForChild("Humanoid",10) if not Humanoid then return end
local DJP=Humanoid.JumpPower
track(Humanoid:GetPropertyChangedSignal("JumpPower"):Connect(function() if not Config['No Jump Cooldown'].Enabled then return end if Humanoid.JumpPower==0 then Humanoid.JumpPower=DJP end end))
end
HeadlessConn=nil;KorbloxOrig={}
function ApplyHeadless(ch)
if HeadlessConn then HeadlessConn:Disconnect() HeadlessConn=nil end
local head=ch:WaitForChild("Head",5) if not head then return end
HeadlessConn=RunService.RenderStepped:Connect(function()
if not ch.Parent or not head.Parent then HeadlessConn:Disconnect() HeadlessConn=nil return end
if Config.Spoofing.Headless then head.LocalTransparencyModifier=1 for _,c in ipairs(head:GetChildren()) do if c:IsA("Decal") then c.Transparency=1 end end
else head.LocalTransparencyModifier=0 for _,c in ipairs(head:GetChildren()) do if c:IsA("Decal") then c.Transparency=0 end end end
end)
end
function ApplyKorblox(ch)
if not ch then return end
local hum=ch:FindFirstChildOfClass("Humanoid") if not hum or hum.RigType~=Enum.HumanoidRigType.R15 then return end
local rf,rl,ru=ch:FindFirstChild("RightFoot"),ch:FindFirstChild("RightLowerLeg"),ch:FindFirstChild("RightUpperLeg")
if not (rf and rl and ru) then return end
if Config.Spoofing.Korblox then
if not KorbloxOrig[ch] then KorbloxOrig[ch]={ru.MeshId,ru.TextureID,ru.Color,ru.Transparency,rl.Transparency,rf.Transparency} end
rf.Transparency=1 rl.Transparency=1 ru.MeshId="http://www.roblox.com/asset/?id=902942096" ru.TextureID="http://roblox.com/asset/?id=902843398" ru.Color=Color3.new(1,1,1) ru.Transparency=0
else
local o=KorbloxOrig[ch] if o then ru.MeshId=o[1] ru.TextureID=o[2] ru.Color=o[3] ru.Transparency=o[4] rl.Transparency=o[5] rf.Transparency=o[6] KorbloxOrig[ch]=nil end
end
end
function HandleSpoofing(ch) if not ch then return end ApplyHeadless(ch) ApplyKorblox(ch) end
pcall(function() if LocalPlayer.Character then WatchCharacterForScripts(LocalPlayer.Character) SetupUtility(LocalPlayer.Character) SetupNoJumpCooldown(LocalPlayer.Character) HandleSpoofing(LocalPlayer.Character) applyTrail();applyMaterialTools() for _,t in pairs(LocalPlayer.Character:GetChildren()) do if t:IsA('Tool') then hookJujuToolFX(t) end end end end)
track(LocalPlayer.CharacterAdded:Connect(function(ch) task.wait(1) pcall(function() WatchCharacterForScripts(ch) SetupUtility(ch) SetupNoJumpCooldown(ch) HandleSpoofing(ch) applyTrail();applyMaterialTools();updateVisualsContinuous() for _,t in pairs(ch:GetChildren()) do if t:IsA('Tool') then hookJujuToolFX(t) end end end) end))
shopItems={};shopNames={}
-- // [修复] 商店扫描改为可重复调用: 脚本比商店先加载时原来会永久扫不到 -> 购买选择栏整个是空的 //
function scanShop()
local shop=getShopFolder()
if not shop then return #shopItems end
local function registerShop(sp)
local nm=string.match(sp.Name,"%b[]")
if not nm and sp.Parent then nm=string.match(sp.Parent.Name,"%b[]") end
if not nm then return end
nm=string.lower(nm):gsub("[%[%]%s]","")
if nm=="" then return end
local head=sp:FindFirstChild("Head") or (sp.Parent and sp.Parent:FindFirstChild("Head"))
local det=sp:FindFirstChildOfClass("ClickDetector") or (sp.Parent and sp.Parent:FindFirstChildOfClass("ClickDetector"))
if head and det and head.Position.Y>-30 then
if not shopNames[nm] then
local item={name=nm,button=head,detector=det}
table.insert(shopItems,item)
shopNames[nm]=item
end
end
end
for _,sp in pairs(shop:GetChildren()) do registerShop(sp) end
for _,sp in pairs(shop:GetDescendants()) do if sp:IsA("Model") or sp:IsA("Part") then registerShop(sp) end end
return #shopItems
end
scanShop()
task.spawn(function()
for _=1,30 do
if Unloaded then return end
if scanShop()>0 then return end
task.wait(1)
end
end)
local GUN_SET={revolver=true,glock=true,silencer=true,deagle=true,shotgun=true,doublereloadsg=true,tacticalshotgun=true,drumshotgun=true,["drum-shotgun"]=true,["double-barrelsg"]=true,smg=true,rifle=true,ak47=true,ar=true,aug=true,drumgun=true,lmg=true,p90=true,flintlock=true}
function shopCategories(force)
if force then scanShop() end
local guns,ammos,others={},{},{}
for _,s in ipairs(shopItems) do
local n=s.name
if n:find("ammo") then table.insert(ammos,n)
elseif GUN_SET[n] then table.insert(guns,n)
else table.insert(others,n) end
end
if #guns+#ammos+#others==0 then
-- // [修复] 商店还没扫到时不再给一个空列表: 退化成"已知物品清单", 点击时 purchaseItem 自己会再扫一次 //
local fallback={}
for n in pairs(GUN_SET) do table.insert(fallback,n) end
for _,n in ipairs({'pistolammo','smgammo','rifleammo','shotgunammo','sniperammo','rpgammo','mediumarmor','smallshield','bigshield'}) do table.insert(fallback,n) end
table.sort(fallback)
return {{name=T("CatAll"),items=fallback}}
end
return {{name=T("CatGuns"),items=guns},{name=T("CatAmmo"),items=ammos},{name=T("CatOther"),items=others}}
end
local function cleanName(n) return string.lower(n):gsub("[%[%]%s]","") end
local function hasItem(item)
local ch=LocalPlayer.Character
if ch then for _,t in pairs(ch:GetChildren()) do if t:IsA("Tool") and cleanName(t.Name)==item then return true end end end
for _,t in pairs(LocalPlayer.Backpack:GetChildren()) do if cleanName(t.Name)==item then return true end end
return false
end
purchasing=false
toastLines={}
local function niceItemName(item)
	item=item or ""
	item=item:gsub("ammo$"," Ammo"):gsub("^%l",string.upper)
	return item
end
function purchaseNotify(text,ok)
local t=Drawing.new("Text")
t.Size=14;t.Font=0;t.Text=text;t.Outline=true;t.Visible=true
t.Color=ok and Color3.fromRGB(120,255,120) or Color3.fromRGB(255,90,90)
table.insert(toastLines,{t=t,born=tick()})
task.delay(4,function() pcall(function() t:Remove() end) for i,x in ipairs(toastLines) do if x.t==t then table.remove(toastLines,i) break end end end)
end
function purchaseItem(item)
if purchasing then return end
local obj=shopNames[item]
if not obj then
local shp=getShopFolder()
if shp then for _,sp in pairs(shp:GetDescendants()) do
local nm=string.match(sp.Name,"%b[]")
if nm then nm=cleanName(nm)
if nm==item then
local head=sp:FindFirstChild("Head") or (sp.Parent and sp.Parent:FindFirstChild("Head"))
local det=sp:FindFirstChildOfClass("ClickDetector")
if head and det then shopNames[item]={name=item,button=head,detector=det} obj=shopNames[item] end
end end end end
end
if not obj then purchaseNotify("Fail: no "..niceItemName(item),false) return end
purchasing=true
task.spawn(function()
local ch=LocalPlayer.Character
local hrp=ch and ch:FindFirstChild("HumanoidRootPart")
if hrp then
local old=hrp.CFrame
pcall(function() obj.detector.MaxActivationDistance=math.huge; obj.detector.RequiresLineOfSight=false end)
hrp.CFrame=obj.button.CFrame-Vector3.new(0,8.8,0)
task.wait(0.15)
local t0=tick()
while not hasItem(item) and tick()-t0<2.5 do
pcall(function() fireclickdetector(obj.detector) end)
hrp.CFrame=obj.button.CFrame-Vector3.new(0,8.8,0)
task.wait(0.1)
end
local got=hasItem(item)
purchaseNotify((got and "Bought " or "Fail: ")..niceItemName(item),got)
task.wait(0.2)
if hrp.Parent then hrp.CFrame=old end
end
purchasing=false
end)
return true
end
local function hookGunAmmo(tool)
local ammo=getToolAmmo(tool)
if ammo then
local old=ammo.Value
track(ammo:GetPropertyChangedSignal("Value"):Connect(function() if ammo.Value<old then shotTime=tick() end old=ammo.Value end))
end
track(tool.Activated:Connect(function() shotTime=tick() end))
end
local function hookCharGuns(ch)
if not ch then return end
for _,t in pairs(ch:GetChildren()) do if t:IsA("Tool") then hookGunAmmo(t) end end
track(ch.ChildAdded:Connect(function(t) if t:IsA("Tool") then hookGunAmmo(t) end end))
end
if LocalPlayer.Character then hookCharGuns(LocalPlayer.Character) end
track(LocalPlayer.CharacterAdded:Connect(hookCharGuns))
local function watchPlayerHits(player)
local function hook(char)
local hum=char:WaitForChild("Humanoid",10) if not hum then return end
local old=hum.Health
track(hum:GetPropertyChangedSignal("Health"):Connect(function()
local h=hum.Health
local diff=old-h
if diff>0 and (recentlyShot() or (localBulletHit[player] and tick()<=localBulletHit[player])) then hitPlayer:Fire(player,char,math.floor(diff)) end
old=h
end))
end
if player.Character then hook(player.Character) end
track(player.CharacterAdded:Connect(hook))
end
for _,pl in pairs(Players:GetPlayers()) do if pl~=LocalPlayer then watchPlayerHits(pl) end end
track(Players.PlayerAdded:Connect(function(pl) if pl~=LocalPlayer then watchPlayerHits(pl) end end))
sounds={["Bubble"]="rbxassetid://6534947588",["Lazer"]="rbxassetid://130791043",["Pick"]="rbxassetid://1347140027",["Pop"]="rbxassetid://198598793",["Rust"]="rbxassetid://1255040462",["Sans"]="rbxassetid://3188795283",["Fart"]="rbxassetid://130833677",["Big"]="rbxassetid://5332005053",["Vine"]="rbxassetid://5332680810",["UwU"]="rbxassetid://8679659744",["Bruh"]="rbxassetid://4578740568",["Skeet"]="rbxassetid://5633695679",["Neverlose"]="rbxassetid://6534948092",["Fatality"]="rbxassetid://6534947869",["Bonk"]="rbxassetid://5766898159",["Minecraft"]="rbxassetid://5869422451",["Gamesense"]="rbxassetid://4817809188",["RIFK7"]="rbxassetid://9102080552",["Bamboo"]="rbxassetid://3769434519",["Crowbar"]="rbxassetid://546410481",["Weeb"]="rbxassetid://6442965016",["Beep"]="rbxassetid://8177256015",["Bambi"]="rbxassetid://8437203821",["Stone"]="rbxassetid://3581383408",["Old Fatality"]="rbxassetid://6607142036",["Click"]="rbxassetid://8053704437",["Ding"]="rbxassetid://7149516994",["Snow"]="rbxassetid://6455527632",["Laser"]="rbxassetid://7837461331",["Mario"]="rbxassetid://2815207981",["Steve"]="rbxassetid://4965083997",["Call of Duty"]="rbxassetid://5952120301",["Bat"]="rbxassetid://3333907347",["TF2 Critical"]="rbxassetid://296102734",["Saber"]="rbxassetid://8415678813",["Baimware"]="rbxassetid://3124331820",["Osu"]="rbxassetid://7149255551",["TF2"]="rbxassetid://2868331684",["Slime"]="rbxassetid://6916371803",["Among Us"]="rbxassetid://5700183626",["One"]="rbxassetid://7380502345"}
beamTextures={["Laser"]="rbxassetid://446111271",["Beam"]="rbxassetid://18854333763"}
function renderTracer(from,to,color,life,olc)
local line=Drawing.new("Line");line.Thickness=1;line.Color=color;line.Transparency=0;line.ZIndex=2;line.Visible=false
local out=Drawing.new("Line");out.Thickness=3;out.Color=olc or Color3.new(0,0,0);out.Transparency=0;out.ZIndex=1;out.Visible=false
local elapsed=0;local fade=0;local alive=true
local con=RunService.Heartbeat:Connect(function(dt)
if not alive then return end
elapsed=elapsed+dt
local p1,ok1=Camera:WorldToViewportPoint(from)
local p2,ok2=Camera:WorldToViewportPoint(to)
if not ok1 or not ok2 then
line.Visible=false;out.Visible=false
return
end
if elapsed>life then
fade=fade+dt
local t=math.clamp(fade/0.2,0,1)
t=t*t*(3-2*t)
line.Transparency=t;out.Transparency=t
end
line.From=Vector2.new(p1.X,p1.Y);line.To=Vector2.new(p2.X,p2.Y)
out.From=line.From;out.To=line.To
line.Visible=true;out.Visible=true
end)
task.delay(life+0.25,function()
alive=false
pcall(function() con:Disconnect() line:Remove() out:Remove() end)
end)
end
function renderBeamTracer(from,to,cfgT)
local life=(cfgT and cfgT.Life) or 0.6
local color=(cfgT and cfgT.Color) or Color3.new(1,1,1)
local tex=beamTextures[(cfgT and cfgT.Texture) or "Laser"] or beamTextures.Laser
local a1=Instance.new("Attachment");a1.Name="HateTA1";a1.CFrame=CFrame.new(from);a1.Parent=Workspace.Terrain
local a2=Instance.new("Attachment");a2.Name="HateTA2";a2.CFrame=CFrame.new(to);a2.Parent=Workspace.Terrain
local beam=Instance.new("Beam")
beam.Name="HateTracer"
beam.Texture=tex
beam.TextureMode=Enum.TextureMode.Wrap
beam.TextureLength=10
beam.FaceCamera=true;beam.LightEmission=1;beam.LightInfluence=1;beam.Enabled=true
beam.Color=ColorSequence.new(color)
beam.Transparency=NumberSequence.new(0)
beam.Width0=0.15;beam.Width1=0.15
beam.Attachment0=a1;beam.Attachment1=a2
local ig=getIgnoredFolder()
beam.Parent=ig or Workspace.Terrain
task.delay(life,function()
pcall(function()
game:GetService("TweenService"):Create(beam,TweenInfo.new(0.2,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),{Transparency=NumberSequence.new(1)}):Play()
end)
task.delay(0.25,function() pcall(function() beam:Destroy() a1:Destroy() a2:Destroy() end) end)
end)
end
function renderTracerNeon(from,to,color,life)
local mid=(from+to)/2
local len=(to-from).Magnitude
local p=Instance.new("Part");p.Name="HateTracer";p.Anchored=true;p.CanCollide=false;p.Size=Vector3.new(0.08,0.08,math.max(len,0.1));p.Color=color;p.Material=Enum.Material.Neon;p.CFrame=CFrame.lookAt(mid,to);p.Parent=Workspace
task.delay(life,function() for i=1,10 do p.Transparency=i/10 task.wait(0.02) end pcall(function() p:Destroy() end) end)
end
function renderTracerByStyle(from,to,cfgT)
local style=cfgT and cfgT.Value or "Line"
if style=="Beam" then renderBeamTracer(from,to,cfgT)
elseif style=="Neon" then renderTracerNeon(from,to,cfgT.Color,cfgT.Life)
else renderTracer(from,to,cfgT.Color,cfgT.Life,cfgT.Outline) end
end
function renderImpact(pos,color,life,size,olc)
local ig=getIgnoredFolder() or Workspace
local p=Instance.new("Part")
p.Name="HateImpact";p.Anchored=true;p.CanCollide=false;p.Size=Vector3.new(size,size,size)
p.Color=color or Color3.new(1,1,1);p.Material=Enum.Material.Neon;p.CFrame=CFrame.new(pos)
p.Parent=ig
local sb=Instance.new("SelectionBox");sb.Adornee=p;sb.Color3=olc or color or Color3.new(1,1,1);sb.LineThickness=0.01;sb.SurfaceTransparency=1;sb.Parent=p
task.delay(life or 0.5,function()
pcall(function()
game:GetService("TweenService"):Create(p,TweenInfo.new(0.2,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),{Transparency=1}):Play()
game:GetService("TweenService"):Create(sb,TweenInfo.new(0.2,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),{Transparency=1}):Play()
end)
task.delay(0.3,function() pcall(function() p:Destroy() end) end)
end)
end
function playHitSound()
local VA=Config['Visual Awareness']
local id
if VA.HitSound.Value=="Custom" then id="rbxassetid://"..VA.HitSound.ID else id=sounds[VA.HitSound.Value] end
if not id then return end
local s=Instance.new("Sound");s.SoundId=id;s.Volume=VA.HitSound.Volume/20;s.PlayOnRemove=true;s.Parent=game:GetService("SoundService")
s:Destroy()
end
function renderDamageNumber(head,damage)
if not head then return end
local VA=Config['Visual Awareness']
local text=Drawing.new("Text")
text.Size=12;text.Font=2;text.Text="-"..tostring(damage);text.Outline=true
text.Color=VA.DamageNumber.Color;text.Visible=false
local position=head.Position
local doFloat=VA.DamageNumber.Value=="Float"
local life=VA.DamageNumber.Life
local elapsed=0
local conn
conn=track(RunService.Heartbeat:Connect(function(dt)
elapsed=elapsed+dt
local pos,on=Camera:WorldToViewportPoint(position)
if on then text.Position=Vector2.new(pos.X,pos.Y-11) text.Visible=true else text.Visible=false end
if elapsed>life then text.Transparency=math.max(1-(elapsed-life)/0.2,0) end
if doFloat then position=position+Vector3.new(0,2.1*dt*2,0) end
end))
task.wait(life+0.2)
conn:Disconnect();pcall(function() text:Remove() end)
end
function renderHitMarker(char)
local VA=Config['Visual Awareness']
local offsets={Vector2.new(1,1),Vector2.new(-1,1),Vector2.new(1,-1),Vector2.new(-1,-1)}
local marks={}
local is3D=VA.HitMarker.Value=="3D"
local base=is3D and char and char:FindFirstChild("HumanoidRootPart") or nil
local elapsed=0
local conn
conn=track(RunService.Heartbeat:Connect(function(dt)
elapsed=elapsed+dt
local center
if base then local p,on=Camera:WorldToViewportPoint(base.Position) if not on then return end center=Vector2.new(p.X,p.Y) else center=UserInputService:GetMouseLocation() end
local tw=elapsed>0.6 and ((elapsed-0.6)/0.12) or 0
for i=1,4 do
local m=marks[i]
if not m then m={l=Drawing.new("Line"),o=Drawing.new("Line")} marks[i]=m end
m.l.Thickness=1;m.l.Color=VA.HitMarker.Color;m.l.ZIndex=2
m.o.Thickness=3;m.o.Color=Color3.new(0,0,0);m.o.ZIndex=1
local off=offsets[i]
m.l.From=center+off*5;m.l.To=m.l.From+off*4
m.o.From=m.l.From;m.o.To=m.l.To
m.l.Transparency=1-tw;m.o.Transparency=1-tw
m.l.Visible=true;m.o.Visible=true
end
end))
task.wait(0.73)
conn:Disconnect()
for _,m in pairs(marks) do pcall(function() m.l:Remove() m.o:Remove() end) end
end
lastCham=nil;lastSkel=nil
function renderHitChams(char)
local VA=Config['Visual Awareness']
pcall(function()
char.Archivable=true
local clone=char:Clone()
char.Archivable=false
for _,p in pairs(clone:GetChildren()) do
if p:IsA("MeshPart") or p:IsA("Part") then
p.CanCollide=false;p.Anchored=true
if VA.HitChams.Value=="Outline" then
p.Transparency=1
local sb=Instance.new("SelectionBox");sb.Adornee=p;sb.Color3=VA.HitChams.Color;sb.LineThickness=0.01;sb.SurfaceTransparency=1;sb.Parent=p
else
p.Material=Enum.Material[VA.HitChams.Value] or Enum.Material.ForceField
p.Color=VA.HitChams.Color
p.Transparency=VA.HitChams.Transparency
end
else p:Destroy() end
end
if VA.HitChams.OnlyLast and lastCham then pcall(function() lastCham:Destroy() end) end
lastCham=clone
clone.Name="\0"
clone.Parent=Workspace
task.wait(VA.HitChams.Life)
if VA.HitChams.FadeOut then
for i=1,10 do for _,p in pairs(clone:GetChildren()) do if p:IsA("Part") or p:IsA("MeshPart") then p.Transparency=i/10 end end task.wait(0.02) end
end
pcall(function() clone:Destroy() end)
end)
end
SKEL_PARTS={"Head","UpperTorso","LowerTorso","LeftUpperArm","LeftHand","RightUpperArm","RightHand","LeftUpperLeg","LeftFoot","RightUpperLeg","RightFoot"}
SKEL_BONES={{"Head","UpperTorso"},{"UpperTorso","LowerTorso"},{"UpperTorso","LeftUpperArm"},{"LeftUpperArm","LeftHand"},{"UpperTorso","RightUpperArm"},{"RightUpperArm","RightHand"},{"LowerTorso","LeftUpperLeg"},{"LeftUpperLeg","LeftFoot"},{"LowerTorso","RightUpperLeg"},{"RightUpperLeg","RightFoot"}}
function renderHitSkeleton(char)
local VA=Config['Visual Awareness']
local positions={}
for _,n in ipairs(SKEL_PARTS) do local p=char:FindFirstChild(n) if p then positions[n]=p.Position end end
if not positions["UpperTorso"] then return end
local lines={}
for _,b in ipairs(SKEL_BONES) do
if positions[b[1]] and positions[b[2]] then
local l=Drawing.new("Line");l.Thickness=1;l.Color=VA.HitSkeleton.Color;l.ZIndex=2;l.Visible=true
local o=Drawing.new("Line");o.Thickness=3;o.Color=Color3.new(0,0,0);o.ZIndex=1;o.Visible=true
table.insert(lines,{l=l,o=o,b=b})
end
end
if VA.HitSkeleton.OnlyLast and lastSkel then pcall(function() for _,d in ipairs(lastSkel) do d.l:Remove() d.o:Remove() end end) lastSkel=nil end
lastSkel=lines
local elapsed=0
local conn
conn=track(RunService.Heartbeat:Connect(function(dt)
elapsed=elapsed+dt
for _,d in ipairs(lines) do
local p1=positions[d.b[1]];local p2=positions[d.b[2]]
local s1,on1=Camera:WorldToViewportPoint(p1)
local s2,on2=Camera:WorldToViewportPoint(p2)
if on1 and on2 then
d.l.From=Vector2.new(s1.X,s1.Y);d.l.To=Vector2.new(s2.X,s2.Y)
d.o.From=d.l.From;d.o.To=d.l.To
d.l.Visible=true;d.o.Visible=true
else d.l.Visible=false;d.o.Visible=false end
end
if elapsed>VA.HitSkeleton.Life then
if VA.HitSkeleton.FadeOut then
local tw=math.max(1-(elapsed-VA.HitSkeleton.Life)/0.2,0)
for _,d in ipairs(lines) do d.l.Transparency=tw d.o.Transparency=tw end
if tw<=0 then conn:Disconnect() pcall(function() for _,d in ipairs(lines) do d.l:Remove() d.o:Remove() end end) end
else conn:Disconnect() pcall(function() for _,d in ipairs(lines) do d.l:Remove() d.o:Remove() end end) end
end
end))
end
particlePart=Instance.new("Part");particlePart.Size=Vector3.new(0.01,0.01,0.01);particlePart.Transparency=1;particlePart.CanCollide=false;particlePart.Anchored=true;particlePart.Parent=game:GetService("CoreGui")
particleTextures={Sparks="rbxassetid://18540695516",Splash="rbxassetid://1084955488",Flame="rbxassetid://11517935503",Bubble="rbxassetid://1084955012",Bits="rbxassetid://8611887361",Air="rbxassetid://11163755167"}
particleEmitters={}
for name,tex in pairs(particleTextures) do
local e=Instance.new("ParticleEmitter")
e.Texture=tex;e.Lifetime=NumberRange.new(0.5,1);e.LightEmission=1;e.Rate=0;e.Speed=NumberRange.new(10,25);e.SpreadAngle=Vector2.new(180,180);e.Enabled=true
e.Name=name;e.Parent=particlePart
particleEmitters[name]=e
end
function renderHitParticle(char)
local VA=Config['Visual Awareness']
local hrp=char:FindFirstChild("HumanoidRootPart") if not hrp then return end
particlePart.CFrame=hrp.CFrame
local e=particleEmitters[VA.HitParticle.Value]
if e then e.Color=ColorSequence.new(VA.HitParticle.Color) e:Emit(20) end
end
track(hitPlayer:Connect(function(player,char,damage)
local VA=Config['Visual Awareness']
if VA.DamageNumber.Enabled then renderDamageNumber(char:FindFirstChild("Head"),damage) end
if VA.HitSound.Enabled then playHitSound() end
if VA.HitMarker.Enabled then renderHitMarker(char) end
if VA.HitChams.Enabled then renderHitChams(char) end
if VA.HitSkeleton.Enabled then renderHitSkeleton(char) end
if VA.HitParticle.Enabled then renderHitParticle(char) end
if VA.Notifications.Enabled then
for _,v in ipairs(VA.Notifications.Value) do
if v=="On hit" then pushNotification("hit "..player.Name.." for "..damage) end
end
end
end))
-- // [juju] 数据层 (L5327-5840): 武器类型表 + 每玩家状态记录 + 本地/敌人子弹信号 //
local gun_types={
["[LMG]"]="automatic",["[Double-Barrel SG]"]="shotgun",["[TacticalShotgun]"]="shotgun",["[AUG]"]="automatic",
["[P90]"]="automatic",["[Glock]"]="pistol",["[DrumGun]"]="automatic",["[Rifle]"]="global",["[Shotgun]"]="shotgun",
["[SMG]"]="automatic",["[AR]"]="automatic",["[Revolver]"]="pistol",["[AK47]"]="automatic",["[SilencerAR]"]="automatic",["[Silencer]"]="pistol"
}
local hatePlayerData={}
newLocalBullet=newSignal()
newEnemyBullet=newSignal()
function updateHatePlayerData(pl)
local d=hatePlayerData[pl]
if not d then d={} hatePlayerData[pl]=d end
local ch=pl and pl.Character
if not ch or not ch.Parent then d.character=nil d.position=nil return d end
d.character=ch
local hrp=ch:FindFirstChild('HumanoidRootPart')
d.position=hrp and hrp.Position or nil
local hum=ch:FindFirstChildOfClass('Humanoid')
d.health=hum and hum.Health or 0
d.max_health=hum and hum.MaxHealth or 100
local armor=ch:FindFirstChild('Armor') or ch:FindFirstChild('armor')
d.armor=(armor and armor.Value) or 0
local tool
for _,t in ipairs(ch:GetChildren()) do if t:IsA('Tool') then tool=t break end end
d.tool=tool
d.knocked=isCharKO(ch)
d.grabbed=ch:FindFirstChild('GRABBING_CONSTRAINT')~=nil
d.forcefield=ch:FindFirstChild('ForceField')~=nil
d.crew=false
return d
end
track(RunService.Heartbeat:Connect(function()
if Unloaded or not Started then return end
for _,pl in ipairs(Players:GetPlayers()) do
if pl~=LocalPlayer then updateHatePlayerData(pl) end
end
end))
track(Players.PlayerRemoving:Connect(function(pl) hatePlayerData[pl]=nil end))
-- // [juju 移植] 子弹: 文件夹名来自 GameCfg(找不到自动扫描), 读取子弹内部偏移拿 Attachment 端点 //
local bulletNames={BULLET_RAYS=true,["Part"]=true,RevStealth=true,bulletray=true,["Bullet"]=true,["bullet"]=true,["Ray"]=true,["Tracer"]=true}
if GameCfg and GameCfg.bulletName and GameCfg.bulletName~='' then bulletNames[GameCfg.bulletName]=true end
local lastShotPosC=nil
local handledBullets=setmetatable({},{__mode='k'})
local function findBulletEnd(obj,beam)
local at
for _,d in ipairs(obj:GetDescendants()) do
if d:IsA("Attachment") and d.CFrame~=(obj.CFrame) then at=d break end
end
if not at and beam then
if beam.Attachment1 then at=beam.Attachment1 end
if not at and beam.Attachment0 then at=beam.Attachment0 end
end
if at then return at.WorldCFrame.Position end
return nil
end
local function handleBullet(obj)
if Unloaded or not obj or handledBullets[obj] then return end
handledBullets[obj]=true
if not obj:IsA("BasePart") then return end
local from=obj.Position
local function findBeam()
local b=obj:FindFirstChildOfClass("Beam")
if b then return b end
for _,d in ipairs(obj:GetDescendants()) do
if d:IsA("Beam") then return d end
end
return nil
end
-- // [修复] 检测瞬间 Beam 还没挂上时最多等 2 帧 (juju 的 wait()); 之后不再要求对象仍在场景里 //
if not (bulletNames[obj.Name] or findBeam()) then
for _=1,2 do
task.wait()
if findBeam() then break end
end
end
local beam=findBeam()
if not beam then return end
local to=findBulletEnd(obj,beam) or (beam.Attachment1 and beam.Attachment1.WorldCFrame.Position or nil)
if not to or (to-from).Magnitude<1 then return end
local hrp=LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
-- // [juju] 本地/敌人判定: recently_shot (弹药减少/开火事件) 或 枪口位置匹配 last_shot_position //
local isLocal=recentlyShot() or (lastShotPosC and (obj.Position-lastShotPosC).Magnitude<1) or (hrp and (obj.Position-hrp.Position).Magnitude<10)
if isLocal then lastShotPosC=obj.Position end
-- // [修复] 本地子弹命中归因: 记录被本地子弹打中的角色, 让命中特效在伤害落地瞬间触发(不再依赖 recentlyShot 0.5s 窗口) //
if isLocal then
local okR,resR=pcall(function()
local rp2=RaycastParams.new()
local f2={}
if LocalPlayer.Character then table.insert(f2,LocalPlayer.Character) end
rp2.FilterDescendantsInstances=f2
rp2.FilterType=Enum.RaycastFilterType.Exclude
return Workspace:Raycast(from,to-from,rp2)
end)
if okR and resR then
local model=resR.Instance and resR.Instance:FindFirstAncestorOfClass('Model')
local pl2=model and Players:GetPlayerFromCharacter(model)
if pl2 and pl2~=LocalPlayer then localBulletHit[pl2]=tick()+1.2 end
end
end
if isLocal then
newLocalBullet:Fire(from,to)
else
newEnemyBullet:Fire(from,to)
end
end
newLocalBullet:Connect(function(from,to)
local VA=Config['Visual Awareness']
if not VA or not from or not to then return end
if VA.Tracers.Enabled then renderTracerByStyle(from,to,VA.Tracers) end
if VA.Impacts.Enabled then renderImpact(to,VA.Impacts.Color,VA.Impacts.Life,VA.Impacts.Size,VA.Impacts.Outline) end
end)
newEnemyBullet:Connect(function(from,to)
local VA=Config['Visual Awareness']
if not VA or not from or not to then return end
if VA.EnemyTracers.Enabled then renderTracerByStyle(from,to,VA.EnemyTracers) end
end)
local bulletFolderWatched=false
local function watchBulletFolder(f)
if not f or bulletFolderWatched then return end
bulletFolderWatched=true
track(f.ChildAdded:Connect(function(o)
if o:IsA("BasePart") and (bulletNames[o.Name] or o:FindFirstChildOfClass("Beam")) then task.spawn(handleBullet,o) end
end))
end
task.spawn(function()
while not Unloaded and not bulletFolderWatched do
task.wait(0.3)
watchBulletFolder(getBulletFolder())
end
end)
-- // [修复] Workspace 兜底监听常开 (即使已找到子弹文件夹): 子弹可能直接创建在 Workspace 下 //
track(Workspace.DescendantAdded:Connect(function(o)
if o:IsA("BasePart") and (bulletNames[o.Name] or o:FindFirstChildOfClass("Beam")) then task.spawn(handleBullet,o) end
end))
-- // ===== PART 1 END ===== //
-- // ===== PART 2 START ===== //
R15_BONES={{"Head","UpperTorso"},{"UpperTorso","LowerTorso"},{"UpperTorso","LeftUpperArm"},{"LeftUpperArm","LeftLowerArm"},{"UpperTorso","RightUpperArm"},{"RightUpperArm","RightLowerArm"},{"LowerTorso","LeftUpperLeg"},{"LeftUpperLeg","LeftLowerLeg"},{"LowerTorso","RightUpperLeg"},{"RightUpperLeg","RightLowerLeg"}}
R6_BONES={{"Head","Torso"},{"Torso","Left Arm"},{"Torso","Right Arm"},{"Torso","Left Leg"},{"Torso","Right Leg"}}
MAX_BONES=10
local ESP_FONT=2
function addESPToPlayer(player)
if player==LocalPlayer then return end
removeESPFromPlayer(player)
local esp={player=player,char=player.Character,nameTag=Drawing.new("Text"),line=Drawing.new("Line"),box=Drawing.new("Square"),boxO=Drawing.new("Square"),fill=Drawing.new("Square"),weaponTag=Drawing.new("Text"),distTag=Drawing.new("Text"),healthBG=Drawing.new("Line"),healthFG=Drawing.new("Line"),healthText=Drawing.new("Text"),armorBar=Drawing.new("Line"),skeleton={},chams=nil}
esp.nameTag.Size=14;esp.nameTag.Center=true;esp.nameTag.Outline=true;esp.nameTag.OutlineColor=Color3.new(0,0,0);esp.nameTag.Font=ESP_FONT;esp.nameTag.Visible=false
esp.line.Visible=false;esp.box.Filled=false;esp.box.Visible=false;esp.boxO.Filled=false;esp.boxO.Visible=false;esp.fill.Filled=true;esp.fill.Visible=false
esp.weaponTag.Size=12;esp.weaponTag.Center=true;esp.weaponTag.Outline=true;esp.weaponTag.Font=ESP_FONT;esp.weaponTag.Color=Color3.fromRGB(255,200,0);esp.weaponTag.Visible=false
esp.distTag.Size=11;esp.distTag.Center=true;esp.distTag.Outline=true;esp.distTag.Font=ESP_FONT;esp.distTag.Visible=false
esp.healthBG.Visible=false;esp.healthFG.Visible=false;esp.healthText.Visible=false;esp.healthText.Font=ESP_FONT;esp.healthText.Outline=true;esp.armorBar.Visible=false
for i=1,MAX_BONES do local l=Drawing.new("Line");l.Visible=false;esp.skeleton[i]=l end
espLabels[player.UserId]=esp
end
function removeESPFromPlayer(player)
local esp=espLabels[player.UserId]
if esp then
pcall(function() esp.nameTag:Remove() esp.line:Remove() esp.box:Remove() esp.boxO:Remove() esp.fill:Remove() esp.weaponTag:Remove() esp.distTag:Remove() esp.healthBG:Remove() esp.healthFG:Remove() esp.healthText:Remove() esp.armorBar:Remove() end)
pcall(function() for _,l in pairs(esp.skeleton) do l:Remove() end end)
pcall(function() if esp.chams then esp.chams:Destroy() end end)
espLabels[player.UserId]=nil
end
end
function hideESP(esp)
esp.nameTag.Visible=false;esp.line.Visible=false;esp.box.Visible=false;esp.boxO.Visible=false;esp.fill.Visible=false;esp.weaponTag.Visible=false;esp.distTag.Visible=false
esp.healthBG.Visible=false;esp.healthFG.Visible=false;esp.healthText.Visible=false;esp.armorBar.Visible=false
for i=1,MAX_BONES do esp.skeleton[i].Visible=false end
end
function refreshESP()
local VA=Config['Visual Awareness']
if Unloaded or PanicMode or not Started or not VA.Enabled then for _,esp in pairs(espLabels) do hideESP(esp) end return end
local myHrp=LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
for userId,esp in pairs(espLabels) do
local player=esp.player
if not player or not player.Parent then removeESPFromPlayer(player) continue end
local ch=player.Character
if esp.char~=ch then esp.char=ch end
if ch and ch.Parent and ch:FindFirstChild("HumanoidRootPart") and ch:FindFirstChild("Head") then
local hum=ch:FindFirstChildOfClass("Humanoid")
if not hum or hum.Health<=0 then hideESP(esp) continue end
if VA.Chams.Enabled then
if not esp.chams then esp.chams=Instance.new("Highlight");esp.chams.Adornee=ch;esp.chams.Parent=game:GetService("CoreGui") end
esp.chams.FillColor=VA.Chams.Color;esp.chams.FillTransparency=VA.Chams.Transparency;esp.chams.OutlineColor=VA.Chams.Color
else if esp.chams then esp.chams:Destroy() esp.chams=nil end end
local ut=ch:FindFirstChild("UpperTorso") or ch.HumanoidRootPart
local inFront=(ut.Position-Camera.CFrame.Position):Dot(Camera.CFrame.LookVector)>0
local above,on=Camera:WorldToViewportPoint(ut.Position+Vector3.new(0,0.5,0))
local below=Camera:WorldToViewportPoint(ut.Position-Vector3.new(0,0.5,0))
if on and inFront and below.Y>above.Y then
local div=below.Y-above.Y
local h=div*6
local w=div*4
local vpos=Vector2.new(below.X-w/2,below.Y-h/2)
local nc=VA.NameTagColor or VA.Color;local bc=VA.Box.Color
-- // [修复] 只要被任一瞄准功能锁定(吸附瞄准 / 瞄准辅助 / Ragebot), 名字+方框立刻变红 //
local lockCol=VA.TargetColor or Color3.fromRGB(255,0,0)
local isLockedTarget=(currentTarget and currentTarget.Parent==ch)
	or (aimAssistPart and aimAssistPart.Parent==ch)
	or (aimbotTargetPart and aimbotTargetPart.Parent==ch)
	or (aimbotTargetPlayer==player)
	or (stickyTargetPlayer==player)
	or (ragebotTarget==player)
if isWhitelisted(player) then nc=VA.WhitelistColor or Color3.fromRGB(80,200,120);bc=VA.WhitelistColor or Color3.fromRGB(80,200,120)
elseif isLockedTarget or table.find(Config.Ragebot.Targets,player.UserId) then nc=lockCol;bc=lockCol
elseif isBlacklisted(player) then nc=VA.BlacklistColor or Color3.fromRGB(255,45,85);bc=VA.BlacklistColor or Color3.fromRGB(255,45,85) end
esp.nameTag.Size=VA.NameTagSize or 14
esp.nameTag.Position=Vector2.new(vpos.X+w/2,vpos.Y-h*0.06-14)
local nm=VA.NameMode or 'Username'
local nmTxt=player.Name
if nm=='DisplayName' then nmTxt=(player.DisplayName and player.DisplayName~="") and player.DisplayName or player.Name
elseif nm=='Username (DisplayName)' then nmTxt=player.Name.." ("..player.DisplayName..")"
elseif nm=='Username (DisplayName) [UserID]' then nmTxt=player.Name.." ("..player.DisplayName..") ["..player.UserId.."]" end
esp.nameTag.Text=nmTxt
esp.nameTag.Outline=VA.Outline
esp.nameTag.Color=nc;esp.nameTag.Visible=VA.Names
if VA.Box.Enabled then
esp.box.Size=Vector2.new(w,h);esp.box.Position=vpos;esp.box.Thickness=VA.Box.Thickness;esp.box.Color=bc;esp.box.Visible=true
esp.boxO.Size=Vector2.new(w+2,h+2);esp.boxO.Position=vpos-Vector2.new(1,1);esp.boxO.Thickness=1;esp.boxO.Color=Color3.new(0,0,0);esp.boxO.Visible=true
else esp.box.Visible=false;esp.boxO.Visible=false end
if VA.Fill.Enabled then esp.fill.Size=Vector2.new(w,h);esp.fill.Position=vpos;esp.fill.Color=VA.Fill.Color;esp.fill.Transparency=VA.Fill.Transparency;esp.fill.Visible=true else esp.fill.Visible=false end
if VA.WeaponESP then
local tool=ch:FindFirstChildOfClass("Tool")
esp.weaponTag.Text=getWeaponDisplayName(tool and tool.Name or nil)
esp.weaponTag.Size=VA.WeaponESPSize or 12
esp.weaponTag.Color=VA.WeaponESPColor or Color3.fromRGB(255,200,0)
esp.weaponTag.Outline=VA.Outline;esp.weaponTag.Position=Vector2.new(vpos.X+w/2,vpos.Y+h+4);esp.weaponTag.Visible=true
else esp.weaponTag.Visible=false end
if VA.Distance and VA.Distance.Enabled and myHrp then
local dist=math.floor((ut.Position-myHrp.Position).Magnitude)
esp.distTag.Text=dist.." studs";esp.distTag.Size=VA.Distance.Size or 11;esp.distTag.Color=VA.Distance.Color or Color3.fromRGB(255,255,255);esp.distTag.Outline=VA.Outline
esp.distTag.Position=Vector2.new(vpos.X+w/2,vpos.Y+h+(VA.WeaponESP and 18 or 4));esp.distTag.Visible=true
else esp.distTag.Visible=false end
if VA.Line.Enabled then
esp.line.Visible=true;esp.line.Color=VA.Line.Color;esp.line.Thickness=VA.Line.Thickness
esp.line.From=Vector2.new(vpos.X+w/2,vpos.Y+h);esp.line.To=Vector2.new(Camera.ViewportSize.X/2,Camera.ViewportSize.Y)
else esp.line.Visible=false end
if VA.HealthBar.Enabled then
local frac=math.clamp(hum.Health/math.max(hum.MaxHealth,1),0,1)
local bx=vpos.X-4
local hpCol=Color3.fromRGB(math.floor(255*(1-frac)),math.floor(255*frac),0)
esp.healthBG.Visible=true;esp.healthBG.From=Vector2.new(bx,vpos.Y+h);esp.healthBG.To=Vector2.new(bx,vpos.Y);esp.healthBG.Thickness=3;esp.healthBG.Color=Color3.fromRGB(35,35,40)
esp.healthFG.Visible=true;esp.healthFG.From=Vector2.new(bx,vpos.Y+h);esp.healthFG.To=Vector2.new(bx,vpos.Y+h-(h*frac));esp.healthFG.Thickness=3;esp.healthFG.Color=hpCol
if VA.HealthBar.ShowText then esp.healthText.Visible=true;esp.healthText.Text=tostring(math.floor(hum.Health+0.5));esp.healthText.Position=Vector2.new(bx-4,vpos.Y+h-(h*frac)-6);esp.healthText.Color=hpCol else esp.healthText.Visible=false end
else esp.healthBG.Visible=false;esp.healthFG.Visible=false;esp.healthText.Visible=false end
if VA.ArmorBar.Enabled then
local be=ch:FindFirstChild(GameCfg.folderName)
local armor=0;local armO=be and be:FindFirstChild(GameCfg.armor);if armO then armor=armO.Value else pcall(function() armor=ch:GetAttribute("Armor") or ch:GetAttribute("ArmorValue") or 0 end) end
esp.armorBar.Visible=true;esp.armorBar.From=Vector2.new(vpos.X+w+4,vpos.Y+h);esp.armorBar.To=Vector2.new(vpos.X+w+4,vpos.Y+h-(h*(armor/130)));esp.armorBar.Thickness=3;esp.armorBar.Color=Color3.fromRGB(255,0,0):Lerp(Color3.fromRGB(0,204,255),math.clamp(armor/130,0,1))
else esp.armorBar.Visible=false end
if VA.Skeleton.Enabled then
local bones=ch:FindFirstChild("UpperTorso") and R15_BONES or (ch:FindFirstChild("Torso") and R6_BONES or nil)
if bones then
for i,b in ipairs(bones) do
local l=esp.skeleton[i]
if l then
local pa,pb=ch:FindFirstChild(b[1]),ch:FindFirstChild(b[2])
if pa and pb then
local s1,o1=Camera:WorldToViewportPoint(pa.Position)
local s2,o2=Camera:WorldToViewportPoint(pb.Position)
if o1 and o2 then l.Visible=true;l.From=Vector2.new(s1.X,s1.Y);l.To=Vector2.new(s2.X,s2.Y);l.Thickness=VA.Skeleton.Thickness;l.Color=VA.Skeleton.Color else l.Visible=false end
else l.Visible=false end
end
end
else for i=1,MAX_BONES do esp.skeleton[i].Visible=false end end
else for i=1,MAX_BONES do esp.skeleton[i].Visible=false end end
else hideESP(esp) end
else hideESP(esp) end
end
end
local function setupESPPlayer(pl)
if pl==LocalPlayer then return end
if pl.Character and pl.Character:FindFirstChild("HumanoidRootPart") then addESPToPlayer(pl) end
pl.CharacterAdded:Connect(function(ch) removeESPFromPlayer(pl) ch:WaitForChild("HumanoidRootPart") task.wait(0.1) if not Unloaded then addESPToPlayer(pl) end end)
pl.CharacterRemoving:Connect(function() removeESPFromPlayer(pl) end)
end
for _,pl in pairs(Players:GetPlayers()) do setupESPPlayer(pl) end
track(Players.PlayerAdded:Connect(setupESPPlayer))
track(Players.PlayerRemoving:Connect(function(pl) removeESPFromPlayer(pl) resolverState[pl]=nil end))
keybindDisplayObjects={}
indicatorPos=Vector2.new(0,40)
indicatorDragging=false;indicatorDragOff=nil;indicatorDragMouse=nil;indicatorDragStart=nil
kdLayout=nil
local FONTMAP={Plex=0,UI=1,Flex=2,Monospace=3}
-- // [修复] 拖动"一卡一卡"的根因: 以前只改 indicatorPos, 真正搬图形要等主 RenderStepped 里 //
-- // 那一整坨(ESP/世界/HUD 全量刷新)跑完才生效, 帧率一掉就一顿一顿. //
-- // 现在: 输入回调里按缓存布局立刻搬图形, 并用和主 UI 一样的"按下点增量"算法, 不跳也不抖. //
function moveIndicatorTo(x,y)
	local lay=kdLayout
	if not lay or #kdRows==0 then return end
	x=math.clamp(x,-40,math.max(Camera.ViewportSize.X-60,60))
	y=math.clamp(y,0,math.max(Camera.ViewportSize.Y-24,24))
	indicatorPos=Vector2.new(x,y)
	for i,r in ipairs(kdRows) do
		local col=math.floor((i-1)/lay.perCol)
		local rowIdx=(i-1)%lay.perCol
		local rx=x+col*(lay.maxW+lay.gap)
		local ry=y+rowIdx*(lay.rowH+lay.gap)
		r.tx.Position=Vector2.new(rx+24,ry+((lay.rowH-r.tx.TextBounds.Y)/2)+1)
		if r.bg then
			r.bg.Position=Vector2.new(rx,ry);r.bg.Size=Vector2.new(lay.maxW,lay.rowH)
			r.bar.Position=Vector2.new(rx,ry);r.bar.Size=Vector2.new(3,lay.rowH)
		end
	end
	kdBounds={x=x,y=y,w=lay.totalW,h=lay.perCol*(lay.rowH+lay.gap)-lay.gap}
end
track(UserInputService.InputBegan:Connect(function(input)
if input.UserInputType~=Enum.UserInputType.MouseButton1 then return end
if not Config['Visual Awareness'].KeybindDisplay then return end
local mp=UserInputService:GetMouseLocation()
local b=kdBounds or {x=indicatorPos.X,y=indicatorPos.Y,w=220,h=40}
if mp.X>=b.x-6 and mp.X<=b.x+b.w+6 and mp.Y>=b.y-6 and mp.Y<=b.y+b.h+6 then
indicatorDragging=true;indicatorDragged=true
indicatorDragMouse=mp
indicatorDragStart=Vector2.new(b.x,b.y)
end
end))
track(UserInputService.InputChanged:Connect(function(input)
if not (indicatorDragging and input.UserInputType==Enum.UserInputType.MouseMovement) then return end
if not (indicatorDragMouse and indicatorDragStart) then return end
local mp=UserInputService:GetMouseLocation()
moveIndicatorTo(indicatorDragStart.X+(mp.X-indicatorDragMouse.X),indicatorDragStart.Y+(mp.Y-indicatorDragMouse.Y))
end))
track(UserInputService.InputEnded:Connect(function(input)
if input.UserInputType==Enum.UserInputType.MouseButton1 then indicatorDragging=false end
end))
-- // [合并] updateKeybindDisplay 统一实现在脚本尾部 "Feature Indicators" 模块 //
sky=Lighting:FindFirstChildOfClass("Sky") or Instance.new("Sky",Lighting)
colorCorr=Lighting:FindFirstChildOfClass("ColorCorrectionEffect") or Instance.new("ColorCorrectionEffect",Lighting)
origLighting={Brightness=Lighting.Brightness,FogEnd=Lighting.FogEnd,ClockTime=Lighting.ClockTime,Saturation=colorCorr.Saturation}
worldAtmosphere=nil
origSky={Bk=sky.SkyboxBk,Dn=sky.SkyboxDn,Ft=sky.SkyboxFt,Lf=sky.SkyboxLf,Rt=sky.SkyboxRt,Up=sky.SkyboxUp}
skyboxes={
["Jungle"]={Bk="http://www.roblox.com/asset/?id=214399891",Dn="http://www.roblox.com/asset/?id=214399887",Ft="http://www.roblox.com/asset/?id=214399894",Lf="http://www.roblox.com/asset/?id=214405668",Rt="http://www.roblox.com/asset/?id=214399899",Up="http://www.roblox.com/asset/?id=214399889"},
["Blossom"]={Bk="http://www.roblox.com/asset/?id=271042516",Dn="http://www.roblox.com/asset/?id=271077243",Ft="http://www.roblox.com/asset/?id=271042556",Lf="http://www.roblox.com/asset/?id=271042310",Rt="http://www.roblox.com/asset/?id=271042467",Up="http://www.roblox.com/asset/?id=271077958"},
["Red night"]={Bk="http://www.roblox.com/Asset/?ID=401664839",Dn="http://www.roblox.com/Asset/?ID=401664862",Ft="http://www.roblox.com/Asset/?ID=401664960",Lf="http://www.roblox.com/Asset/?ID=401664881",Rt="http://www.roblox.com/Asset/?ID=401664901",Up="http://www.roblox.com/Asset/?ID=401664936"},
["Purple default"]={Bk="http://www.roblox.com/asset/?id=13694952867",Dn="http://www.roblox.com/asset/?id=13694968325",Ft="http://www.roblox.com/asset/?id=13694980654",Lf="http://www.roblox.com/asset/?id=13694998113",Rt="http://www.roblox.com/asset/?id=13695002700",Up="http://www.roblox.com/asset/?id=13695007103"},
["Foggy"]={Bk="rbxassetid://1370717244",Dn="rbxassetid://1370717336",Ft="rbxassetid://1370717438",Lf="rbxassetid://1370717567",Rt="rbxassetid://1370717698",Up="rbxassetid://1370717782"},
}
function applyWorld()
local VA=Config['Visual Awareness']
if VA.WorldMod.Enabled then
Lighting.Brightness=VA.WorldMod.Brightness;Lighting.FogEnd=VA.WorldMod.FogEnd;Lighting.ClockTime=VA.WorldMod.ClockTime;colorCorr.Saturation=VA.WorldMod.Saturation
else
Lighting.Brightness=origLighting.Brightness;Lighting.FogEnd=origLighting.FogEnd;Lighting.ClockTime=origLighting.ClockTime;colorCorr.Saturation=origLighting.Saturation
end
if VA.WorldMod.Enabled and VA.WorldMod.Atmosphere then
if not worldAtmosphere then worldAtmosphere=Instance.new("Atmosphere",Lighting) end
worldAtmosphere.Color=VA.WorldMod.AtmosphereColor;worldAtmosphere.Decay=VA.WorldMod.AtmosphereDecay;worldAtmosphere.Density=VA.WorldMod.AtmosphereDensity;worldAtmosphere.Glare=VA.WorldMod.AtmosphereGlare;worldAtmosphere.Haze=VA.WorldMod.AtmosphereHaze
elseif worldAtmosphere then worldAtmosphere:Destroy();worldAtmosphere=nil end
if VA.Skybox.Enabled then local sb=skyboxes[VA.Skybox.Value] if sb then sky.SkyboxBk=sb.Bk;sky.SkyboxDn=sb.Dn;sky.SkyboxFt=sb.Ft;sky.SkyboxLf=sb.Lf;sky.SkyboxRt=sb.Rt;sky.SkyboxUp=sb.Up end
else sky.SkyboxBk=origSky.Bk;sky.SkyboxDn=origSky.Dn;sky.SkyboxFt=origSky.Ft;sky.SkyboxLf=origSky.Lf;sky.SkyboxRt=origSky.Rt;sky.SkyboxUp=origSky.Up end
end
aspectMult=CFrame.new(0,0,0,1,0,0,0,1,0,0,0,1)
function applyAspect() aspectMult=CFrame.new(0,0,0,1,0,0,0,Config['Visual Awareness'].AspectRatio.Value/100,0,0,0,1) end
crossLines={}
for i=1,4 do crossLines[i]={l=Drawing.new("Line"),o=Drawing.new("Line")} end
watermarkText=Drawing.new("Text");watermarkText.Visible=false
notifications={}
function pushNotification(text)
local ttl=Drawing.new("Text");ttl.Size=13;ttl.Font=2;ttl.Text="hate";ttl.Outline=true;ttl.OutlineColor=Color3.new(0,0,0);ttl.Color=Color3.fromRGB(124,110,255);ttl.Visible=true;ttl.ZIndex=13
local t=Drawing.new("Text");t.Size=13;t.Font=2;t.Text=text;t.Outline=true;t.OutlineColor=Color3.new(0,0,0);t.Color=Color3.new(1,1,1);t.Visible=true;t.ZIndex=13
local bg=Drawing.new("Square");bg.Filled=true;bg.Color=Color3.fromRGB(16,16,22);bg.Transparency=0.05;bg.Visible=true;bg.ZIndex=10
local edge=Drawing.new("Square");edge.Filled=true;edge.Color=Color3.fromRGB(124,110,255);edge.Transparency=0;edge.Visible=true;edge.ZIndex=11
table.insert(notifications,{t=t,ttl=ttl,bg=bg,edge=edge,born=tick()})
task.delay(4,function() for _,o in ipairs({ttl,t,bg,edge}) do pcall(function() o:Remove() end) end for i,n in ipairs(notifications) do if n.t==t then table.remove(notifications,i) break end end end)
end
crossPos=Vector2.new(0,0)
function updateHudDraws(dt)
local VA=Config['Visual Awareness']
if VA.Crosshair.Enabled and not PanicMode and Started then
local target=VA.Crosshair.Follow and (currentTarget or aimAssistPart) or nil
local desired
if target then local p,on=Camera:WorldToViewportPoint(target.Position) if on then desired=Vector2.new(p.X,p.Y) end end
if not desired then desired=VA.Crosshair.Location=="Mouse" and UserInputService:GetMouseLocation() or Camera.ViewportSize/2 end
local sm=VA.Crosshair.Smooth==0 and 1 or math.min(dt*(20*(1.25-VA.Crosshair.Smooth/100)),1)
crossPos=crossPos:Lerp(desired,sm)
local spin=VA.Crosshair.Spin==0 and 0 or (tick()*VA.Crosshair.Spin*0.05)
local angs={0,1.57,3.14,4.71}
for i=1,4 do
local cl=crossLines[i]
local dir=Vector2.new(math.cos(spin+angs[i]),math.sin(spin+angs[i]))
cl.l.Thickness=1;cl.l.Color=VA.Crosshair.Color;cl.l.ZIndex=10000
cl.o.Thickness=3;cl.o.Color=Color3.new(0,0,0);cl.o.ZIndex=9999
cl.l.From=crossPos+dir*VA.Crosshair.Gap;cl.l.To=cl.l.From+dir*VA.Crosshair.Size
cl.o.From=crossPos+dir*(VA.Crosshair.Gap-1);cl.o.To=cl.o.From+dir*(VA.Crosshair.Size+2)
cl.l.Visible=true;cl.o.Visible=true
end
else for i=1,4 do crossLines[i].l.Visible=false;crossLines[i].o.Visible=false end end
if VA.Watermark.Enabled and not PanicMode and Started then
watermarkText.Visible=true;watermarkText.Text=VA.Watermark.Text;watermarkText.Color=VA.Watermark.Color;watermarkText.Size=VA.Watermark.Size;watermarkText.Outline=true
local pos=VA.Watermark.Position=="Mouse" and UserInputService:GetMouseLocation() or Vector2.new(Camera.ViewportSize.X/2-40,20)
watermarkText.Position=pos+Vector2.new(0,VA.Watermark.YOffset)
else watermarkText.Visible=false end
for i,n in ipairs(notifications) do
local y=16+VA.Notifications.YOffset+(i-1)*34
local w=math.max(260,n.t.TextBounds.X+n.ttl.TextBounds.X+40)
n.bg.Position=Vector2.new(15,y);n.bg.Size=Vector2.new(w,28)
n.edge.Position=Vector2.new(15,y);n.edge.Size=Vector2.new(3,28)
n.ttl.Position=Vector2.new(27,y+6)
n.t.Position=Vector2.new(27+n.ttl.TextBounds.X+9,y+6)
end
local vp=Camera.ViewportSize
for i,x in ipairs(toastLines) do x.t.Position=Vector2.new(vp.X-280,vp.Y-30-(#toastLines-i)*18) end
end
local moneyLast=0
track(RunService.RenderStepped:Connect(function()
if Unloaded or not Started then return end
local VA=Config['Visual Awareness']
if not VA.MoneyText.Enabled then return end
if tick()-moneyLast<1 then return end
moneyLast=tick()
pcall(function()
local msg=LocalPlayer.PlayerGui:FindFirstChild("MainScreenGui")
if not msg then return end
local mt=msg:FindFirstChild("MoneyText")
if not mt then return end
mt.ClipsDescendants=false
mt.TextColor3=VA.MoneyText.Color
if VA.MoneyText.Value=="Simple" then mt.AnchorPoint=Vector2.new(1,1);mt.Position=UDim2.new(1,-10,1,-10);mt.AutomaticSize=Enum.AutomaticSize.X;mt.Size=UDim2.new(0,0,0,20);mt.TextSize=24
else mt.AnchorPoint=Vector2.new(0,0);mt.Position=UDim2.new(1,-210,1,-60);mt.Size=UDim2.new(0,200,0,50);mt.TextSize=25 end
if VA.MoneyText.Image~="None" then
local img=mt:FindFirstChild("MelodyImg")
if not img then img=Instance.new("ImageLabel");img.Name="MelodyImg";img.BackgroundTransparency=1;img.AnchorPoint=Vector2.new(0,0.5);img.Position=UDim2.new(0,-28,0.5,0);img.Size=UDim2.new(0,24,0,24);img.ZIndex=10;img.Parent=mt end
img.Image=VA.MoneyText.Image=="My Melody" and "rbxassetid://18401067020" or ""
else
local img=mt:FindFirstChild("MelodyImg") if img then img:Destroy() end
end
end)
end))
local statLast=0
track(RunService.RenderStepped:Connect(function()
if Unloaded or not Started then return end
local VA=Config['Visual Awareness']
if not VA.StatBars.Enabled then return end
if tick()-statLast<2 then return end
statLast=tick()
pcall(function()
local msg=LocalPlayer.PlayerGui:FindFirstChild("MainScreenGui")
if not msg then return end
local bar=msg:FindFirstChild("Bar")
if not bar then return end
for _,obj in ipairs(bar:GetChildren()) do
local b=obj:FindFirstChild("bar");local fb=obj:FindFirstChild("firebar")
local nm=obj.Name
if (nm=="HP" or nm=="Health") and b then b.BackgroundColor3=VA.StatBars.HP end
if (nm=="Energy" or nm=="Stamina") and b then b.BackgroundColor3=VA.StatBars.Energy end
if nm=="Armor" and b then b.BackgroundColor3=VA.StatBars.Armor end
if nm=="Armor" and fb then fb.BackgroundColor3=VA.StatBars.Fire end
if VA.StatBars.Value=="Minimalistic" then
if not obj:FindFirstChild("hudCorner") then Instance.new("UICorner",obj).Name="hudCorner" end
if b and not b:FindFirstChild("hudCorner") then Instance.new("UICorner",b).Name="hudCorner" end
obj.BackgroundTransparency=0.5
elseif VA.StatBars.Value=="Flat" then obj.BackgroundColor3=Color3.fromRGB(24,24,24)
elseif VA.StatBars.Value=="Gamesense" then obj.BackgroundColor3=Color3.fromRGB(20,20,20)
elseif VA.StatBars.Value=="Minecraft" then obj.BackgroundTransparency=1
elseif VA.StatBars.Value=="Sanrio" then obj.BackgroundColor3=nm=="HP" and Color3.fromRGB(255,0,4) or nm=="Energy" and Color3.fromRGB(255,233,110) or Color3.fromRGB(0,163,212) end
end
end)
end))
local hotLast=0
track(RunService.RenderStepped:Connect(function()
if Unloaded or not Started then return end
local VA=Config['Visual Awareness']
if not VA.Hotbar.Enabled then return end
if tick()-hotLast<2 then return end
hotLast=tick()
pcall(function()
local hotbar=nil
local cg=game:GetService("CoreGui")
if cg:FindFirstChild("RobloxGui") and cg.RobloxGui:FindFirstChild("Backpack") then hotbar=cg.RobloxGui.Backpack:FindFirstChild("Hotbar") end
if not hotbar then
local msg=LocalPlayer.PlayerGui:FindFirstChild("MainScreenGui")
if msg then hotbar=msg:FindFirstChild("Hotbar") end
end
if not hotbar then return end
for _,obj in ipairs(hotbar:GetChildren()) do
if obj:IsA("Frame") or obj:IsA("TextButton") then
if VA.Hotbar.Value=="Minimalistic" then
if not obj:FindFirstChild("hbCorner") then local c=Instance.new("UICorner");c.CornerRadius=UDim.new(0,6);c.Name="hbCorner";c.Parent=obj end
if not obj:FindFirstChild("hbStroke") then local s=Instance.new("UIStroke");s.Thickness=2;s.Transparency=0.56;s.Name="hbStroke";s.Parent=obj end
else
if obj:FindFirstChild("hbCorner") then obj.hbCorner:Destroy() end
if obj:FindFirstChild("hbStroke") then obj.hbStroke:Destroy() end
end
end
end
end)
end))
origZoom=LocalPlayer.CameraMaxZoomDistance
function applyView()
local VA=Config['Visual Awareness']
pcall(function() LocalPlayer.CameraMaxZoomDistance=VA.View.UnlockZoom and 9e9 or origZoom end)
pcall(function() UserInputService.MouseIconEnabled=not VA.View.HideCursor end)
pcall(function() local chat=LocalPlayer.PlayerGui:FindFirstChild("Chat") if chat and chat:FindFirstChild("Frame") then chat.Frame.Visible=VA.View.ShowChat end end)
pcall(function()
local msg=LocalPlayer.PlayerGui:FindFirstChild("MainScreenGui")
if msg then local aim=msg:FindFirstChild("Aim") if aim then
aim.Size=VA.View.HideGunCrosshair and UDim2.new(0,0,0,0) or UDim2.new(0,4,0,4)
for _,c in ipairs(aim:GetChildren()) do if c:IsA("Frame") then c.BackgroundTransparency=VA.View.HideGunCrosshair and 1 or 0 else c.ImageTransparency=VA.View.HideGunCrosshair and 1 or 0 end end
end end end)
end
cfg('Visual Awareness CustomShoot',{Enabled=false,Value='SSG-08',ID='',Volume=1})
savedShoot={}
function applyShootSoundTool(tool)
local h=tool:FindFirstChild("Handle") if not h then return end
local snd=h:FindFirstChildOfClass("Sound") if not snd then return end
if not savedShoot[tool] then savedShoot[tool]={snd.SoundId,snd.Volume} end
local VA=Config['Visual Awareness CustomShoot']
if VA.Enabled then snd.SoundId=VA.Value=="Custom" and ("rbxassetid://"..VA.ID) or (sounds[VA.Value] or snd.SoundId);snd.Volume=VA.Volume
else local o=savedShoot[tool] if o then snd.SoundId=o[1];snd.Volume=o[2] end end
end
local function hookCharSounds(ch)
if not ch then return end
for _,t in pairs(ch:GetChildren()) do if t:IsA("Tool") then applyShootSoundTool(t) end end
track(ch.ChildAdded:Connect(function(t) if t:IsA("Tool") then applyShootSoundTool(t) end end))
end
if LocalPlayer.Character then hookCharSounds(LocalPlayer.Character) end
track(LocalPlayer.CharacterAdded:Connect(hookCharSounds))
teleportAngle=0
function teleportToFace(player)
local ch=LocalPlayer.Character if not ch then return end
local hrp=ch:FindFirstChild("HumanoidRootPart") if not hrp then return end
if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then hrp.CFrame=player.Character.HumanoidRootPart.CFrame*CFrame.new(0,0,-2) end
end
function updateTeleport(dt)
if Unloaded or not Started or not Config.Teleport.Enabled then return end
local mode=Config.Teleport.Mode
if mode~='Follow' and mode~='Orbit' then return end
local ch=LocalPlayer.Character if not ch then return end
local hrp=ch:FindFirstChild("HumanoidRootPart") if not hrp then return end
local tp=nil
for _,p in pairs(Players:GetPlayers()) do if p~=LocalPlayer and p.Character and p.Character:FindFirstChild("HumanoidRootPart") and Config.Teleport.Target==p.UserId then tp=p break end end
if not tp then return end
local tHRP=tp.Character:FindFirstChild("HumanoidRootPart") if not tHRP then return end
local dist=Config.Teleport.Distance;local spd=math.clamp(Config.Teleport.Speed,0,50)
if mode=='Follow' then
local cf=tHRP.CFrame
local targetPos=cf.Position+cf.LookVector*(-dist)+Vector3.new(0,0.5,0)
local cur=hrp.Position;local delta=targetPos-cur;local d=delta.Magnitude;local step=spd*10*dt
if spd>=50 or d<=step or d<0.001 then hrp.CFrame=CFrame.new(targetPos) else hrp.CFrame=CFrame.new(cur+delta.Unit*step) end
else
teleportAngle=teleportAngle+dt*(spd*0.08)
hrp.CFrame=CFrame.new(tHRP.Position+Vector3.new(math.cos(teleportAngle)*dist,2,math.sin(teleportAngle)*dist))
end
end
track(RunService.Heartbeat:Connect(function(dt)
if Unloaded or not Started then return end
local ch=LocalPlayer.Character
local hrp=ch and ch:FindFirstChild("HumanoidRootPart")
local hum=ch and ch:FindFirstChildOfClass("Humanoid")
if hrp and hum then
local MV=Config.Movement
speedActive=MV.CFrameSpeed and bindActive('Speed')
if speedActive then hrp.CFrame=hrp.CFrame+hum.MoveDirection*MV.SpeedValue*dt end
flyActive=MV.CFrameFly and bindActive('Fly')
if flyActive then
local md=hum.MoveDirection;local vert=0
if UserInputService:IsKeyDown(Enum.KeyCode.Space) then vert=1 end
if UserInputService:IsKeyDown(Enum.KeyCode.LeftControl) then vert=-1 end
hrp.CFrame=hrp.CFrame+Vector3.new(md.X,0,md.Z)*MV.FlyValue*dt+Vector3.new(0,vert*MV.FlyValue*dt,0)
hrp.Velocity=Vector3.new(hrp.Velocity.X,1.8,hrp.Velocity.Z)
end
if MV.Noclip then for _,p in pairs(ch:GetChildren()) do if p:IsA("Part") or p:IsA("MeshPart") then p.CanCollide=false end end end
if MV.PreventFling then local v=hrp.Velocity if v.Y>50 or v.Y<-50 then hrp.Velocity=Vector3.new(v.X,0,v.Z) end if v.Magnitude>200 then hrp.Velocity=v.Unit*200 end end
end
if Config['Super Jump'].Enabled and hum and hrp and bindActive('Super Jump') then
local k=true
if k then hrp.Velocity=Vector3.new(hrp.Velocity.X,Config['Super Jump'].Power,hrp.Velocity.Z);task.wait(Config['Super Jump'].Cooldown) end
end
updateTeleport(dt)
end))
track(RunService.Stepped:Connect(function()
if Unloaded or not Started then return end
local ch=LocalPlayer.Character
if ch and Config.Movement.Noclip then for _,p in pairs(ch:GetChildren()) do if p:IsA("Part") or p:IsA("MeshPart") then p.CanCollide=false end end end
end))
track(RunService.RenderStepped:Connect(function(dt)
if Unloaded or not Started then return end
if currentTarget then local p=Players:GetPlayerFromCharacter(currentTarget.Parent) if p and isWhitelisted(p) then currentTarget=nil;isLocking=false end end
if isSelfKnocked() and isLocking then currentTarget=nil;isLocking=false end
if Config['Hitbox Expander'].Enabled then
for _,pl in pairs(Players:GetPlayers()) do
if pl~=LocalPlayer and pl.Character and not isWhitelisted(pl) then
local h=pl.Character:FindFirstChild("HumanoidRootPart")
if h then h.Size=Vector3.new(Config['Hitbox Expander'].Size,Config['Hitbox Expander'].Size,Config['Hitbox Expander'].Size);h.Transparency=1 end
end
end
end
updateFOVCircle();updateLockLine();refreshESP();applyWorld();updateHudDraws(dt);updateVisualsContinuous()
updateKeybindDisplay()
if Config['Sticky'].Enabled then
if stickyLocked then currentTarget=getStickyLockPart() end
else stickyLocked=false;stickyTargetPlayer=nil;currentTarget=nil end
if not aimApplyBound then applyAimbot(dt) end
updateAimFOV()
end))
-- // [juju] 宽高比: 直接沿用 juju 原版 camera.CFrame*=multiplier (独立连接, 不受其他功能报错影响) //
track(RunService.RenderStepped:Connect(function()
if Unloaded or not Started then return end
if Config['Visual Awareness'].AspectRatio.Enabled then
pcall(function() Camera.CFrame=Camera.CFrame*aspectMult end)
end
end))
track(RunService.RenderStepped:Connect(function()
if Unloaded or not Started then return end
if not Config['Rapid Fire'].Enabled or not rapidFireActive then return end
if tick()-lastRapidShot<Config['Rapid Fire'].Delay then return end
local ch=LocalPlayer.Character if not ch then return end
local tool=ch:FindFirstChildOfClass("Tool") if not tool then return end
if not rapidPatched[tool] then
rapidPatched[tool]=true
pcall(function()
for _,v in ipairs(getconnections(tool.Activated)) do
local fi=debug.getinfo(v.Function)
for i=1,fi.nups do
local c,n=debug.getupvalue(v.Function,i)
if type(c)=="number" then debug.setupvalue(v.Function,i,0.0000000000001) end
end
end
end)
end
if Config['Rapid Fire'].SpecificWeapons.Enabled then
local v=false
for _,w in pairs(Config['Rapid Fire'].SpecificWeapons.Weapons) do if tool.Name==w then v=true break end end
if not v then return end
end
tool:Activate();lastRapidShot=tick()
end))
-- // [新] Rapid Fire v2 (HyperFire) //
track(game.DescendantAdded:Connect(function(obj)
if Config['Rapid Fire v2'].Enabled and obj.Name=='ToleranceCooldown' and obj:IsA('ValueBase') then obj.Value=0 end
end))
track(RunService.RenderStepped:Connect(function()
if Unloaded or not Started then return end
if not Config['Rapid Fire v2'].Enabled then return end
if not UserInputService:IsMouseButtonPressed(Enum.UserInputType.MouseButton1) then return end
local ch=LocalPlayer.Character if not ch then return end
local tool=ch:FindFirstChildOfClass('Tool') if not tool or not tool:FindFirstChild('Ammo') then return end
tool:Activate()
end))
-- // [新] Remove Shoot Animations (free.txt) //
local ShootAnimIds={["rbxassetid://2807049953"]=true,["rbxassetid://2809413000"]=true,["rbxassetid://2809419094"]=true,["rbxassetid://507768375"]=true,["rbxassetid://507755388"]=true,["rbxassetid://2877910736"]=true}
track(RunService.RenderStepped:Connect(function()
if Unloaded or not Started then return end
if not Config['Remove Shoot Animations'].Enabled then return end
for _,plr in ipairs(Players:GetPlayers()) do
local pch=plr.Character
local phum=pch and pch:FindFirstChildOfClass('Humanoid')
if phum then for _,tr in ipairs(phum:GetPlayingAnimationTracks()) do if ShootAnimIds[tr.Animation and tr.Animation.AnimationId] then pcall(function() tr:Stop() end) end end end
end
end))
track(RunService.RenderStepped:Connect(function()
if Unloaded or not Started then return end
local irOn=(Config['Infinite Range'] and Config['Infinite Range'].Enabled==true) or (Config.Ragebot and Config.Ragebot.InfiniteRange==true)
if irOn~=infRangeActive then infRangeActive=irOn end
if not irOn then return end
local ch=LocalPlayer.Character if not ch then return end
local tool=ch:FindFirstChildOfClass("Tool") if not tool then return end
if tool~=irState.tool or tick()-irState.lastScan>2 then irState.tool=tool;irState.lastScan=tick();irScan(tool) end
if tick()-irState.lastMod>3 then irState.lastMod=tick();irPatchModules() end
local maxR=Config['Infinite Range'].MaxRange
for _,rv in ipairs(irState.vals) do pcall(function() rv.Value=maxR end) end
for _,a in ipairs(irState.attrs) do pcall(function() a.inst:SetAttribute(a.name,maxR) end) end
pcall(function() tool:SetAttribute("Range",maxR) end)
pcall(function() for _,d in pairs(tool:GetDescendants()) do if (d:IsA("NumberValue") or d:IsA("IntValue")) and nameLooksLikeRange(d.Name) then d.Value=maxR end end end)
end))
track(RunService.RenderStepped:Connect(function()
if Unloaded or not Started then return end
if not Config['Delay Changer'].Enabled then return end
local ch=LocalPlayer.Character if not ch then return end
local dv=Config['Delay Changer'].Delay
for _,tool in pairs(ch:GetChildren()) do
if tool:IsA("Tool") then
local apply=false
if not Config['Delay Changer'].SpecificWeapons.Enabled then apply=true
else for _,w in pairs(Config['Delay Changer'].SpecificWeapons.Weapons) do if tool.Name==w then apply=true break end end end
if apply then
local cd=tool:FindFirstChild("ShootingCooldown")
if cd then cd.Value=dv end
pcall(function() tool:SetAttribute("ShootingCooldown",dv) end)
end
end
end
end))
track(RunService.RenderStepped:Connect(function()
if Unloaded or not Started then return end
local ch=LocalPlayer.Character if not ch then return end
local tool=ch:FindFirstChildOfClass("Tool") if not tool then return end
local ammo=getToolAmmo(tool)
if ammo and ammo.Value==0 then
if Config.Utility.SmartAutoReload then
task.wait(Config.Utility.SmartAutoReloadDelay)
local ammo2=getToolAmmo(tool)","if ch:FindFirstChildOfClass("Tool")==tool and ammo2 and ammo2.Value==0 then
local ev=getMainEvent()
if ev then ev:FireServer("Reload",tool) end
end
elseif Config.Utility.AutoReload then
local ev=getMainEvent()
if ev then ev:FireServer("Reload",tool) end
end
end
end))
lastAmmoBuy=0
track(RunService.RenderStepped:Connect(function()
if Unloaded or not Started then return end
if not Config['Auto Ammo'].Enabled then return end
if purchasing then return end
if tick()-lastAmmoBuy<2 then return end
local ch=LocalPlayer.Character if not ch then return end
local tool=ch:FindFirstChildOfClass("Tool") if not tool then return end
local mag=tool:FindFirstChild("Magazine") or tool:FindFirstChild("CurrentAmmo") or tool:FindFirstChild("Mag") or tool:FindFirstChild("Clip")
local ammoVal=(mag and mag:IsA("ValueBase")) and mag or getToolAmmo(tool)
if not ammoVal then return end
if ammoVal.Value<=Config['Auto Ammo'].Amount then
lastAmmoBuy=tick()
buyAmmo(tool.Name)
end
end))
-- // [新] Auto Armor (juju 式) //
local lastArmorBuy=0
track(RunService.Heartbeat:Connect(function()
if Unloaded or not Started then return end
if not Config.Purchases.AutoArmor then return end
if purchasing then return end
if tick()-lastArmorBuy<3 then return end
local ch=LocalPlayer.Character if not ch then return end
local be=ch:FindFirstChild(GameCfg.folderName) if not be then return end
local a=be:FindFirstChild(GameCfg.armor) if not a then return end
local mx=130
if a.Value/mx <= Config.Purchases.ArmorAt/100 then
lastArmorBuy=tick()
purchaseItem("mediumarmor")
end
end))
-- // [修复] 按键绑定: Toggle=切换主开关(与UI同步), Hold=按住生效 //
-- // [重构] 按键输入分发: Gate=激活门(不动UI主开关) / Hold=按住 / Action=一次性动作 //
function runBindAction(name)
if name=='Target Lock' then
if not Config['Sticky'].Enabled then Config['Sticky'].Enabled=true notifyToggle("Sticky",true) refreshAllComponents() end
if stickyLocked then stickyLocked=false;stickyTargetPlayer=nil;currentTarget=nil;isLocking=false;stickyTracer.Visible=false
else lockStickyTarget() end
elseif name=='Emote' then
if not Config['Emote Bind'].Enabled then return end
local hum=LocalPlayer.Character and LocalPlayer.Character:FindFirstChildOfClass("Humanoid")
if hum then
local ids={["Happier Jump"]="rbxassetid://15609995579",["Bouncy Twirl"]="rbxassetid://14352343065",["V Pose"]="rbxassetid://10214319518"}
local anim=Instance.new("Animation");anim.AnimationId=ids[Config.Movement.Emote] or ids["Happier Jump"]
emoteTrack=hum:LoadAnimation(anim);emoteTrack:Play()
end
elseif name=='Purchase Armor' then
purchaseItem("mediumarmor")
elseif name=='Auto Buy' then
if not Config['Auto Buy'].Enabled then return end
local list=Config['Auto Buy'].Items or {}
task.spawn(function()
for _,it in ipairs(list) do
while purchasing do task.wait(0.1) end
purchaseItem(it)
task.wait(0.2)
end
end)
end
end
track(UserInputService.InputBegan:Connect(function(input)
if Unloaded or not Started then return end
if WaitingForKey or BindConsumed then return end
if isTyping() then return end
if matchInput(Config.Keybinds['UI Toggle'],input) then toggleMenu() return end
if not bindHas('UI Toggle') and input.KeyCode==Enum.KeyCode.RightShift then toggleMenu() return end
if input.KeyCode==Enum.KeyCode.F9 then
PanicMode=not PanicMode
if PanicMode and GuiOpen then closeMenu() end
updateKeybindDisplay()
return
end
local didBind=false
for _,name in ipairs(BIND_ORDER) do
if matchInput(Config.Keybinds[name],input) then
didBind=true
local kind=bindKind(name)
if kind=='Hold' then holdStates[name]=true
elseif kind=='Action' then runBindAction(name)
else toggleBindArm(name) end
end
end
if didBind then
refreshAllComponents()
updateKeybindDisplay()
return
end
if input.UserInputType==Enum.UserInputType.MouseButton1 then rapidFireActive=true end
end))
track(UserInputService.InputEnded:Connect(function(input)
if Unloaded or not Started then return end
for _,name in ipairs(BIND_ORDER) do
if matchInput(Config.Keybinds[name],input) and bindKind(name)=='Hold' then holdStates[name]=false end
end
if matchInput(Config.Keybinds['Target Lock'],input) and Config.Keybinds['Target Lock'].Mode=='Hold' then isLocking=false;currentTarget=nil end
if matchInput(Config.Keybinds['Emote'],input) then if emoteTrack then emoteTrack:Stop();emoteTrack=nil end end
if input.UserInputType==Enum.UserInputType.MouseButton1 then rapidFireActive=false end
updateKeybindDisplay()
end))
-- // [主题] 模仿 juju UI 框架: 纯黑描边 / 直角 / 左侧图标导航栏 //
UI={BG=Color3.fromRGB(10,10,10),Top=Color3.fromRGB(12,12,12),Panel=Color3.fromRGB(14,14,14),Panel2=Color3.fromRGB(23,23,23),Stroke=Color3.fromRGB(40,40,40),Text=Color3.fromRGB(205,205,205),TextDim=Color3.fromRGB(109,109,109),Accent=Color3.fromRGB(124,110,255),ToggleOff=Color3.fromRGB(77,77,77),Green=Color3.fromRGB(80,200,120),Danger=Color3.fromRGB(230,70,90),Sidebar=Color3.fromRGB(9,9,9),Hover=Color3.fromRGB(30,30,30),Line=Color3.fromRGB(40,40,40)}
if Config['UI Settings'].ThemeColor then UI.Accent=Config['UI Settings'].ThemeColor end
AccentElements={}
ScreenGui=Instance.new("ScreenGui");ScreenGui.Name="HateUI";ScreenGui.ResetOnSpawn=false;ScreenGui.ZIndexBehavior=Enum.ZIndexBehavior.Sibling;ScreenGui.DisplayOrder=999999
pcall(function() ScreenGui.IgnoreGuiInset=true end)
do local gp=false
if not gp and gethui then pcall(function() ScreenGui.Parent=gethui();gp=true end) end
if not gp then pcall(function() ScreenGui.Parent=game:GetService("CoreGui");gp=true end) end
if not gp then pcall(function() ScreenGui.Parent=LocalPlayer:WaitForChild("PlayerGui");gp=true end) end
-- // [修复] 弹窗专用顶层 Gui: 之前弹窗和主 UI 同层, 层级/透明度互相干扰, 列表被压住看起来就是"空的" //
PopupGui=Instance.new("ScreenGui");PopupGui.Name="HatePopup";PopupGui.ResetOnSpawn=false;PopupGui.ZIndexBehavior=Enum.ZIndexBehavior.Global;PopupGui.DisplayOrder=9999999
pcall(function() PopupGui.IgnoreGuiInset=true end)
PopupParent=PopupGui
do local pp=false
if not pp and gethui then pcall(function() PopupGui.Parent=gethui();pp=true end) end
if not pp then pcall(function() PopupGui.Parent=game:GetService("CoreGui");pp=true end) end
if not pp then pcall(function() PopupGui.Parent=LocalPlayer:WaitForChild("PlayerGui");pp=true end) end
if not PopupGui.Parent then PopupParent=ScreenGui;PopupGui=nil end
end
end
hudGui=Instance.new("ScreenGui")
pcall(function() hudGui.Parent=game:GetService("CoreGui") end)
if not hudGui.Parent then pcall(function() hudGui.Parent=LocalPlayer:WaitForChild("PlayerGui") end) end
function curT() return math.clamp(Config['UI Settings'].Transparency,0,80)/100 end
function applyUITransparency()
local t=curT()
pcall(function() for _,o in ipairs(ScreenGui:GetDescendants()) do if (o:IsA("Frame") or o:IsA("TextButton") or o:IsA("TextBox") or o:IsA("ScrollingFrame")) and o.BackgroundTransparency<1 and not o:IsDescendantOf(PopupParent) then o.BackgroundTransparency=t end end end)
end
function fontEnum(name) local ok,f=pcall(function() return Enum.Font[name] end) return (ok and f) or Enum.Font.Code end
function applyFontAll()
local f=UI_Font
for _,gui in ipairs({ScreenGui,hudGui}) do pcall(function() for _,o in ipairs(gui:GetDescendants()) do if (o:IsA("TextLabel") or o:IsA("TextButton") or o:IsA("TextBox")) and o.Name~="HateBold" then o.Font=f end end end) end
end
function setAccentColor(v)
local old=UI.Accent
UI.Accent=v
Config['UI Settings'].ThemeColor=v
for _,e in pairs(AccentElements) do pcall(function() if e:IsA("TextLabel") or e:IsA("TextButton") then e.TextColor3=v elseif e:IsA("Frame") then e.BackgroundColor3=v end end) end
-- // [修复] 选中颜色必须整UI生效: 描边/未登记的按钮/标题等全部跟随主题换色 //
if old~=v then
local white=Color3.fromRGB(255,255,255)
for _,gui in ipairs({ScreenGui,hudGui,PopupGui}) do
if gui and gui.Parent then
pcall(function()
for _,o in ipairs(gui:GetDescendants()) do
if o:IsA("UIStroke") then
if o.Color==old then o.Color=v end
elseif (o:IsA("TextLabel") or o:IsA("TextButton")) then
if not o.RichText and o.TextColor3==old and not (old==white) then o.TextColor3=v end
elseif (o:IsA("Frame") or o:IsA("ScrollingFrame") or o:IsA("TextBox")) then
if o.BackgroundColor3==old then o.BackgroundColor3=v end
end
end
end)
end
end
end
if applyTabVisual then pcall(function() applyTabVisual(activeTab) end) end
refreshAllComponents()
end
function updateRainbow()
local en=Config['UI Settings'].Rainbow
if en and not rainbowConn then
rainbowConn=RunService.RenderStepped:Connect(function(dt) if Unloaded then return end rainbowHue=(rainbowHue+dt*0.08)%1 setAccentColor(Color3.fromHSV(rainbowHue,0.65,1)) end)
elseif not en and rainbowConn then rainbowConn:Disconnect();rainbowConn=nil end
end
UISPEED=0.16
function tweenUI(o,t,ti) pcall(function() TweenService:Create(o,TweenInfo.new(ti or UISPEED,Enum.EasingStyle.Sine,Enum.EasingDirection.Out),t):Play() end) end
SIDEBAR_W=92;TOPBAR_H=36;BOTTOM_H=24
do
MainFrame=Instance.new("Frame");MainFrame.Size=UDim2.new(0,780,0,540);MainFrame.Position=UDim2.new(0.5,-390,0.5,-270)
MainFrame.BackgroundColor3=UI.BG;MainFrame.BorderSizePixel=0;MainFrame.Visible=false;MainFrame.ClipsDescendants=false;MainFrame.Parent=ScreenGui
local ms=Instance.new("UIStroke");ms.Color=UI.Stroke;ms.Thickness=1;ms.Parent=MainFrame
TopBar=Instance.new("Frame");TopBar.Size=UDim2.new(1,0,0,TOPBAR_H);TopBar.BackgroundColor3=UI.Top;TopBar.BorderSizePixel=0;TopBar.Parent=MainFrame
local tbLine=Instance.new("Frame");tbLine.Size=UDim2.new(1,0,0,1);tbLine.Position=UDim2.new(0,0,1,-1);tbLine.BackgroundColor3=UI.Line;tbLine.BorderSizePixel=0;tbLine.Parent=TopBar
local Dragging,DragInput,MousePos,FramePos
UserInputService.InputChanged:Connect(function(Input) if Input==DragInput and Dragging then local D=Input.Position-MousePos MainFrame.Position=UDim2.new(FramePos.X.Scale,FramePos.X.Offset+D.X,FramePos.Y.Scale,FramePos.Y.Offset+D.Y) end end)
TopBar.InputBegan:Connect(function(Input) if Input.UserInputType==Enum.UserInputType.MouseButton1 then Dragging=true;MousePos=Input.Position;FramePos=MainFrame.Position Input.Changed:Connect(function() if Input.UserInputState==Enum.UserInputState.End then Dragging=false end end) end end)
TopBar.InputChanged:Connect(function(Input) if Input.UserInputType==Enum.UserInputType.MouseMovement then DragInput=Input end end)
local TitleLbl=Instance.new("TextLabel");TitleLbl.Name="HateBold";TitleLbl.Size=UDim2.new(0,300,1,0);TitleLbl.Position=UDim2.new(0,12,0,0)
TitleLbl.BackgroundTransparency=1;TitleLbl.RichText=true;TitleLbl.Font=Enum.Font.GothamBold;TitleLbl.TextSize=15;TitleLbl.TextXAlignment=Enum.TextXAlignment.Left
TitleLbl.Text='<font color="rgb(124,110,255)">hate</font><font color="rgb(205,205,205)">.CC</font><font color="rgb(60,60,60)">  /  </font><font color="rgb(109,109,109)">da hood</font>';TitleLbl.Parent=TopBar
local VerLbl=Instance.new("TextLabel");VerLbl.Size=UDim2.new(0,200,1,0);VerLbl.Position=UDim2.new(1,-212,0,0)
VerLbl.BackgroundTransparency=1;VerLbl.Font=Enum.Font.Code;VerLbl.TextSize=11;VerLbl.TextXAlignment=Enum.TextXAlignment.Right;VerLbl.TextColor3=UI.TextDim;VerLbl.Text="hate.CC";VerLbl.Parent=TopBar
Sidebar=Instance.new("Frame");Sidebar.Size=UDim2.new(0,SIDEBAR_W,1,-(TOPBAR_H+BOTTOM_H));Sidebar.Position=UDim2.new(0,0,0,TOPBAR_H);Sidebar.BackgroundColor3=UI.Sidebar;Sidebar.BorderSizePixel=0;Sidebar.Parent=MainFrame
local sbLine=Instance.new("Frame");sbLine.Size=UDim2.new(0,1,1,0);sbLine.Position=UDim2.new(1,-1,0,0);sbLine.BackgroundColor3=UI.Line;sbLine.BorderSizePixel=0;sbLine.Parent=Sidebar
local logo=Instance.new("TextLabel");logo.Name="HateBold";logo.Size=UDim2.new(1,0,0,38);logo.Position=UDim2.new(0,0,0,4);logo.BackgroundTransparency=1;logo.Font=Enum.Font.GothamBlack;logo.TextSize=16;logo.Text="hate.CC";logo.TextColor3=UI.Accent;logo.Parent=Sidebar;table.insert(AccentElements,logo)
local logoSub=Instance.new("TextLabel");logoSub.Size=UDim2.new(1,0,0,12);logoSub.Position=UDim2.new(0,0,0,42);logoSub.BackgroundTransparency=1;logoSub.Font=Enum.Font.Code;logoSub.TextSize=9;logoSub.Text="da hood";logoSub.TextColor3=UI.TextDim;logoSub.Parent=Sidebar
TabBar=Instance.new("Frame");TabBar.Size=UDim2.new(1,0,1,-58);TabBar.Position=UDim2.new(0,0,0,58);TabBar.BackgroundTransparency=1;TabBar.Parent=Sidebar
local tll=Instance.new("UIListLayout");tll.FillDirection=Enum.FillDirection.Vertical;tll.Padding=UDim.new(0,2);tll.SortOrder=Enum.SortOrder.LayoutOrder;tll.Parent=TabBar
local BottomBar=Instance.new("Frame");BottomBar.Size=UDim2.new(1,0,0,BOTTOM_H);BottomBar.Position=UDim2.new(0,0,1,-BOTTOM_H);BottomBar.BackgroundColor3=UI.Top;BottomBar.BorderSizePixel=0;BottomBar.Parent=MainFrame
local bbLine=Instance.new("Frame");bbLine.Size=UDim2.new(1,0,0,1);bbLine.BackgroundColor3=UI.Line;bbLine.BorderSizePixel=0;bbLine.Parent=BottomBar
local DateLbl=Instance.new("TextLabel");DateLbl.Size=UDim2.new(0.5,-10,1,0);DateLbl.Position=UDim2.new(0,10,0,0)
DateLbl.BackgroundTransparency=1;DateLbl.Text=os.date("%Y-%m-%d");DateLbl.TextColor3=UI.TextDim;DateLbl.Font=Enum.Font.Code;DateLbl.TextSize=10;DateLbl.TextXAlignment=Enum.TextXAlignment.Left;DateLbl.Parent=BottomBar
UserIdLabel=Instance.new("TextLabel");UserIdLabel.Size=UDim2.new(0.5,-10,1,0);UserIdLabel.Position=UDim2.new(0.5,0,0,0)
local UserLbl=UserIdLabel
UserLbl.BackgroundTransparency=1;UserLbl.RichText=true;UserLbl.Font=Enum.Font.Code;UserLbl.TextSize=10;UserLbl.TextXAlignment=Enum.TextXAlignment.Right
UserLbl.Text='user <font color="rgb(205,205,205)">'..LocalPlayer.Name..'</font>';UserLbl.Parent=BottomBar
function applyHideUserId()
if not UserIdLabel then return end
UserIdLabel.Visible=(Config['UI Settings'].HideUserId~=true)
end
ContentFrame=Instance.new("Frame");ContentFrame.Size=UDim2.new(1,-SIDEBAR_W,1,-(TOPBAR_H+BOTTOM_H));ContentFrame.Position=UDim2.new(0,SIDEBAR_W,0,TOPBAR_H);ContentFrame.BackgroundTransparency=1;ContentFrame.Parent=MainFrame
local function addResize(px,py)
local h=Instance.new("TextButton");h.Size=UDim2.new(0,14,0,14);h.AnchorPoint=Vector2.new(px,py);h.Position=UDim2.new(px,0,py,0);h.BackgroundTransparency=1;h.BorderSizePixel=0;h.ZIndex=6;h.Text="";h.Parent=MainFrame
h.MouseButton1Down:Connect(function()
local startSize=MainFrame.AbsoluteSize;local startPos=MainFrame.AbsolutePosition
local startMouse=UserInputService:GetMouseLocation()
local conn;conn=RunService.RenderStepped:Connect(function()
local mp=UserInputService:GetMouseLocation()
local dx=mp.X-startMouse.X;local dy=mp.Y-startMouse.Y
local w=startSize.X;local hh=startSize.Y
if px==1 then w=startSize.X+dx else w=startSize.X-dx end
if py==1 then hh=startSize.Y+dy else hh=startSize.Y-dy end
w=math.clamp(w,560,1400);hh=math.clamp(hh,380,900)
local newX=startPos.X;local newY=startPos.Y
if px==0 then newX=startPos.X+(startSize.X-w) end
if py==0 then newY=startPos.Y+(startSize.Y-hh) end
MainFrame.Size=UDim2.new(0,w,0,hh)
MainFrame.Position=UDim2.fromOffset(newX,newY)
end)
local up;up=UserInputService.InputEnded:Connect(function(inp) if inp.UserInputType==Enum.UserInputType.MouseButton1 then conn:Disconnect();up:Disconnect() end end)
end)
end
addResize(1,1);addResize(0,1);addResize(1,0);addResize(0,0)
end
function addStroke(o,c) local s=Instance.new("UIStroke");s.Color=c or UI.Stroke;s.Thickness=1;s.Parent=o return s end
function CreatePage()
local page=Instance.new("Frame");page.Size=UDim2.new(1,-14,1,-14);page.Position=UDim2.new(0,7,0,7);page.BackgroundTransparency=1;page.Visible=false;page.Parent=ContentFrame
local colL=Instance.new("ScrollingFrame");colL.Size=UDim2.new(0.5,-4,1,0);colL.BackgroundTransparency=1;colL.BorderSizePixel=0;colL.ScrollBarThickness=2;colL.ScrollBarImageColor3=UI.Accent;colL.AutomaticCanvasSize=Enum.AutomaticSize.Y;colL.CanvasSize=UDim2.new();colL.Parent=page
local colR=Instance.new("ScrollingFrame");colR.Size=UDim2.new(0.5,-4,1,0);colR.Position=UDim2.new(0.5,8,0,0);colR.BackgroundTransparency=1;colR.BorderSizePixel=0;colR.ScrollBarThickness=2;colR.ScrollBarImageColor3=UI.Accent;colR.AutomaticCanvasSize=Enum.AutomaticSize.Y;colR.CanvasSize=UDim2.new();colR.Parent=page
Instance.new("UIListLayout",colL).Padding=UDim.new(0,8)
Instance.new("UIListLayout",colR).Padding=UDim.new(0,8)
return page,colL,colR
end
Pages={}
do local a,b,c=CreatePage();Pages.Aim={root=a,L=b,R=c}
a,b,c=CreatePage();Pages.Visuals={root=a,L=b,R=c}
a,b,c=CreatePage();Pages.Misc={root=a,L=b,R=c}
a,b,c=CreatePage();Pages.Players={root=a,L=b,R=c}
a,b,c=CreatePage();Pages.Settings={root=a,L=b,R=c} end
TabButtons={}
activeTab="Aim"
function applyTabVisual(k)
if not k then k=activeTab end
activeTab=k
for key,p in pairs(Pages) do p.root.Visible=(key==k) end
for key,b in pairs(TabButtons) do
local on=(key==k)
b.underline.Visible=on
b.lbl.TextColor3=on and UI.Text or UI.TextDim
b.icon.TextColor3=on and UI.Accent or UI.TextDim
if b._on~=on then b._on=on tweenUI(b.btn,{BackgroundColor3=on and UI.Panel or UI.Sidebar}) end
end
end
TAB_ICONS={Aim="●",Visuals="◆",Misc="■",Players="▲",Settings="◇"}
function CreateSidebarTab(key,langKey,order)
local btn=Instance.new("TextButton");btn.Size=UDim2.new(1,0,0,50);btn.LayoutOrder=order or 1;btn.Text="";btn.AutoButtonColor=false;btn.BorderSizePixel=0;btn.BackgroundColor3=UI.Sidebar;btn.Parent=TabBar
local icon=Instance.new("TextLabel");icon.Name="HateBold";icon.Size=UDim2.new(1,0,0,20);icon.Position=UDim2.new(0,0,0,7);icon.BackgroundTransparency=1;icon.Font=Enum.Font.GothamBold;icon.TextSize=15;icon.Text=(TAB_ICONS and TAB_ICONS[key]) or "*";icon.TextColor3=UI.TextDim;icon.Parent=btn
local lbl=Instance.new("TextLabel");lbl.Size=UDim2.new(1,0,0,13);lbl.Position=UDim2.new(0,0,0,29);lbl.BackgroundTransparency=1;lbl.Font=Enum.Font.Code;lbl.TextSize=10;lbl.TextXAlignment=Enum.TextXAlignment.Center;lbl.TextColor3=UI.TextDim;lbl.Parent=btn;registerLang(lbl,langKey)
local ul=Instance.new("Frame");ul.Size=UDim2.new(0,2,0,26);ul.Position=UDim2.new(0,0,0.5,-13);ul.BackgroundColor3=UI.Accent;ul.BorderSizePixel=0;ul.Visible=false;ul.Parent=btn
table.insert(AccentElements,ul)
local sep=Instance.new("Frame");sep.Size=UDim2.new(1,-16,0,1);sep.Position=UDim2.new(0,8,1,-1);sep.BackgroundColor3=UI.Line;sep.BorderSizePixel=0;sep.Parent=btn
TabButtons[key]={btn=btn,lbl=lbl,icon=icon,underline=ul}
btn.MouseButton1Click:Connect(function() applyTabVisual(key) end)
btn.MouseEnter:Connect(function() if activeTab~=key then tweenUI(btn,{BackgroundColor3=UI.Hover}) end end)
btn.MouseLeave:Connect(function() if activeTab~=key then tweenUI(btn,{BackgroundColor3=UI.Sidebar}) end end)
end
CreateSidebarTab("Aim","TabAim",1);CreateSidebarTab("Visuals","TabVisuals",2);CreateSidebarTab("Misc","TabMisc",3);CreateSidebarTab("Players","TabPlayers",4);CreateSidebarTab("Settings","TabSettings",5)
applyTabVisual("Aim")
GuiOpen=false
function closeDropdown() if DropdownPopup then pcall(function() DropdownPopup.frame:Destroy() end);pcall(function() DropdownPopup.catcher:Destroy() end);DropdownPopup=nil end end
ColorPopup=nil;ColorCatcher=nil
function closeColorPopup() if ColorPopup then pcall(function() ColorPopup:Destroy() end) ColorPopup=nil end if ColorCatcher then pcall(function() ColorCatcher:Destroy() end) ColorCatcher=nil end end
function closeGridPopup()
local gp=GridPopup
GridPopup=nil
if gp then
pcall(function() if gp.conn then gp.conn:Disconnect() end end)
pcall(function() if gp.c then gp.c:Destroy() end end)
pcall(function() if gp.f then gp.f:Destroy() end end)
end
end
function openMenu()
GuiOpen=true
local w=MainFrame.Size.X.Offset;local h=MainFrame.Size.Y.Offset
if w<20 then w=780;h=540 end
MainFrame.Visible=true
MainFrame.BackgroundTransparency=1
MainFrame.Size=UDim2.new(0,math.floor(w*0.95),0,math.floor(h*0.95))
task.delay(0.02,function() tweenUI(MainFrame,{BackgroundTransparency=0,Size=UDim2.new(0,w,0,h)},0.2) end)
applyUITransparency()
end
function closeMenu() GuiOpen=false;MainFrame.Visible=false;MainFrame.BackgroundTransparency=0
pcall(function() if KeybindPopup then KeybindPopup:Destroy() end end) KeybindPopup=nil;WaitingForKey=nil;closeDropdown();closeColorPopup();closeGridPopup() end
function toggleMenu() if GuiOpen then closeMenu() else openMenu() end end
UIComponents={}
function registerComponent(fn) table.insert(UIComponents,fn) end
function refreshAllComponents() for _,u in ipairs(UIComponents) do pcall(u) end end
function CreateSection(col,langKey)
local wrap=Instance.new("Frame");wrap.BackgroundTransparency=1;wrap.AutomaticSize=Enum.AutomaticSize.Y;wrap.Size=UDim2.new(1,0,0,0);wrap.Parent=col
local lay=Instance.new("UIListLayout");lay.Padding=UDim.new(0,2);lay.Parent=wrap
local hdr=Instance.new("Frame");hdr.Size=UDim2.new(1,0,0,22);hdr.BackgroundColor3=UI.Top;hdr.BorderSizePixel=0;hdr.Parent=wrap
local hb=Instance.new("Frame");hb.Size=UDim2.new(1,0,0,1);hb.Position=UDim2.new(0,0,1,-1);hb.BackgroundColor3=UI.Line;hb.BorderSizePixel=0;hb.Parent=hdr
local dot=Instance.new("Frame");dot.Size=UDim2.new(0,2,0,10);dot.Position=UDim2.new(0,5,0.5,-5);dot.BackgroundColor3=UI.Accent;dot.BorderSizePixel=0;dot.Parent=hdr;table.insert(AccentElements,dot)
local hl=Instance.new("TextLabel");hl.Name="HateBold";hl.Size=UDim2.new(1,-24,1,0);hl.Position=UDim2.new(0,12,0,0);hl.BackgroundTransparency=1;hl.TextXAlignment=Enum.TextXAlignment.Left;hl.TextColor3=UI.Text;hl.Font=Enum.Font.GothamBold;hl.TextSize=12;hl.Parent=hdr
registerLang(hl,langKey)
local box=Instance.new("Frame");box.Size=UDim2.new(1,0,0,0);box.AutomaticSize=Enum.AutomaticSize.Y;box.BackgroundColor3=UI.Panel;box.BorderSizePixel=0;box.Parent=wrap;addStroke(box)
local bl=Instance.new("UIListLayout");bl.Padding=UDim.new(0,2);bl.Parent=box
local bp=Instance.new("UIPadding");bp.PaddingTop=UDim.new(0,5);bp.PaddingBottom=UDim.new(0,5);bp.PaddingLeft=UDim.new(0,5);bp.PaddingRight=UDim.new(0,5);bp.Parent=box
return box
end
function CreateLabel(parent,text)
local row=Instance.new("Frame");row.Size=UDim2.new(1,0,0,14);row.BackgroundTransparency=1;row.Parent=parent
local l=Instance.new("TextLabel");l.Size=UDim2.new(1,-12,1,0);l.Position=UDim2.new(0,8,0,0);l.BackgroundTransparency=1;l.Text=text;l.TextColor3=UI.TextDim;l.Font=UI_Font;l.TextSize=10;l.TextXAlignment=Enum.TextXAlignment.Left;l.TextWrapped=true;l.Parent=row
return row
end
-- // [新增] 会实时刷新的说明文字 (显示辅助瞄准当前锁到的目标) //
function CreateDynLabel(parent,fn)
local row=Instance.new("Frame");row.Size=UDim2.new(1,0,0,14);row.BackgroundTransparency=1;row.Parent=parent
local l=Instance.new("TextLabel");l.Size=UDim2.new(1,-12,1,0);l.Position=UDim2.new(0,8,0,0);l.BackgroundTransparency=1;l.TextColor3=UI.TextDim;l.Font=UI_Font;l.TextSize=10;l.TextXAlignment=Enum.TextXAlignment.Left;l.TextWrapped=true;l.Parent=row
local o={row=row,text=l}
function o:Refresh() local ok,t=pcall(fn) if ok then l.Text=t or "" end end
o:Refresh()
return o
end

function CreateToggle(parent,langKey,GetFunc,SetFunc)
local row=Instance.new("TextButton");row.Size=UDim2.new(1,0,0,20);row.BackgroundColor3=UI.Hover;row.BackgroundTransparency=1;row.Text="";row.AutoButtonColor=false;row.BorderSizePixel=0;row.Parent=parent
local box=Instance.new("Frame");box.Size=UDim2.new(0,10,0,10);box.Position=UDim2.new(0,5,0.5,-5);box.BackgroundColor3=UI.BG;box.BorderSizePixel=0;box.Parent=row
addStroke(box,UI.ToggleOff)
local bin=Instance.new("Frame");bin.Size=UDim2.new(1,-2,1,-2);bin.Position=UDim2.new(0,1,0,1);bin.BackgroundColor3=UI.ToggleOff;bin.BorderSizePixel=0;bin.Parent=box
local lbl=Instance.new("TextLabel");lbl.Size=UDim2.new(1,-26,1,0);lbl.Position=UDim2.new(0,21,0,0);lbl.BackgroundTransparency=1;lbl.Font=UI_Font;lbl.TextSize=12;lbl.TextXAlignment=Enum.TextXAlignment.Left;lbl.Parent=row
registerLang(lbl,langKey)
local function Update() local en=GetFunc() bin.BackgroundColor3=en and UI.Accent or UI.ToggleOff lbl.TextColor3=en and UI.Text or UI.TextDim end
Update();registerComponent(Update)
row.MouseEnter:Connect(function() tweenUI(row,{BackgroundTransparency=0.82}) end)
row.MouseLeave:Connect(function() tweenUI(row,{BackgroundTransparency=1}) end)
row.MouseButton1Click:Connect(function() SetFunc(not GetFunc());Update() end)
return row,lbl
end
function CreateSlider(parent,langKey,Min,Max,GetFunc,SetFunc)
local function G() local v=GetFunc() if type(v)~="number" then v=Min end return v end
local function rel() return math.clamp((G()-Min)/(Max-Min),0,1) end
local row=Instance.new("Frame");row.Size=UDim2.new(1,0,0,30);row.BackgroundTransparency=1;row.Parent=parent
local lbl=Instance.new("TextLabel");lbl.Size=UDim2.new(0.62,-6,0,12);lbl.Position=UDim2.new(0,5,0,1);lbl.BackgroundTransparency=1;lbl.TextColor3=UI.TextDim;lbl.Font=UI_Font;lbl.TextSize=11;lbl.TextXAlignment=Enum.TextXAlignment.Left;lbl.Parent=row;registerLang(lbl,langKey)
local val=Instance.new("TextLabel");val.Size=UDim2.new(0.38,-4,0,12);val.Position=UDim2.new(0.62,0,0,1);val.BackgroundTransparency=1;val.Text=tostring(G());val.TextColor3=UI.Text;val.Font=Enum.Font.Code;val.TextSize=11;val.TextXAlignment=Enum.TextXAlignment.Right;val.Parent=row
local trackBar=Instance.new("Frame");trackBar.Size=UDim2.new(1,-10,0,3);trackBar.Position=UDim2.new(0,5,1,-11);trackBar.BackgroundColor3=UI.Panel2;trackBar.BorderSizePixel=0;trackBar.Parent=row
local fill=Instance.new("Frame");fill.Size=UDim2.new(rel(),0,1,0);fill.BackgroundColor3=UI.Accent;fill.BorderSizePixel=0;fill.Parent=trackBar;table.insert(AccentElements,fill)
local dot=Instance.new("Frame");dot.Size=UDim2.new(0,3,0,11);dot.Position=UDim2.new(rel(),-1,0.5,-5.5);dot.BackgroundColor3=UI.Accent;dot.BorderSizePixel=0;dot.ZIndex=2;dot.Parent=trackBar;table.insert(AccentElements,dot)
local hit=Instance.new("Frame");hit.Size=UDim2.new(1,-10,0,14);hit.Position=UDim2.new(0,5,1,-16);hit.BackgroundTransparency=1;hit.Parent=row
local function Update() local v=G();val.Text=tostring(v);local r=rel();fill.Size=UDim2.new(r,0,1,0);dot.Position=UDim2.new(r,-1,0.5,-5.5) end
Update();registerComponent(Update)
local function apply(px) local r=math.clamp((px-trackBar.AbsolutePosition.X)/trackBar.AbsoluteSize.X,0,1) local nv=math.floor(Min+(Max-Min)*r+0.5);SetFunc(nv);Update() end
hit.InputBegan:Connect(function(i)
if i.UserInputType==Enum.UserInputType.MouseButton1 then
apply(i.Position.X)
local mc=UserInputService.InputChanged:Connect(function(mi) if mi.UserInputType==Enum.UserInputType.MouseMovement then apply(mi.Position.X) end end)
i.Changed:Connect(function() if i.UserInputState==Enum.UserInputState.End then pcall(function() mc:Disconnect() end) end end)
end end)
end
function openDropdown(anchorBtn,options,onSet)
closeDropdown()
local catcher=Instance.new("TextButton");catcher.Size=UDim2.new(1,0,1,0);catcher.BackgroundTransparency=1;catcher.Text="";catcher.ZIndex=80;catcher.Parent=PopupParent
local h=8+#options*20
local frame=Instance.new("Frame");frame.Size=UDim2.new(0,math.max(anchorBtn.AbsoluteSize.X,130),0,h)
frame.Position=UDim2.fromOffset(anchorBtn.AbsolutePosition.X,math.min(anchorBtn.AbsolutePosition.Y+anchorBtn.AbsoluteSize.Y+2,Camera.ViewportSize.Y-h-4))
frame.BackgroundColor3=UI.BG;frame.BackgroundTransparency=curT();frame.BorderSizePixel=0;frame.ZIndex=90;frame.Parent=PopupParent;addStroke(frame,UI.Accent)
local lay=Instance.new("UIListLayout");lay.Padding=UDim.new(0,1);lay.Parent=frame
for _,opt in ipairs(options) do
local ob=Instance.new("TextButton");ob.Size=UDim2.new(1,0,0,19);ob.BackgroundColor3=UI.Panel;ob.BorderSizePixel=0;ob.Text="   "..tostring(opt);ob.TextXAlignment=Enum.TextXAlignment.Left;ob.TextColor3=UI.Text;ob.Font=UI_Font;ob.TextSize=11;ob.ZIndex=91;ob.AutoButtonColor=false;ob.Parent=frame
ob.MouseEnter:Connect(function() tweenUI(ob,{BackgroundColor3=UI.Hover}) end)
ob.MouseLeave:Connect(function() tweenUI(ob,{BackgroundColor3=UI.Panel}) end)
ob.MouseButton1Click:Connect(function() onSet(opt);closeDropdown() end)
end
catcher.MouseButton1Click:Connect(closeDropdown)
DropdownPopup={frame=frame,catcher=catcher}
end
function CreateDropdown(parent,langKey,Options,GetFunc,SetFunc)
local row=Instance.new("Frame");row.Size=UDim2.new(1,0,0,24);row.BackgroundTransparency=1;row.Parent=parent
local lbl=Instance.new("TextLabel");lbl.Size=UDim2.new(0.45,-6,1,0);lbl.Position=UDim2.new(0,5,0,0);lbl.BackgroundTransparency=1;lbl.TextXAlignment=Enum.TextXAlignment.Left;lbl.TextColor3=UI.TextDim;lbl.Font=UI_Font;lbl.TextSize=12;lbl.Parent=row;registerLang(lbl,langKey)
local btn=Instance.new("TextButton");btn.Size=UDim2.new(0.55,-5,0,18);btn.Position=UDim2.new(0.45,0,0.5,-9);btn.BackgroundColor3=UI.Panel2;btn.BorderSizePixel=0;btn.Text="";btn.AutoButtonColor=false;btn.Parent=row;addStroke(btn)
local val=Instance.new("TextLabel");val.Size=UDim2.new(1,-18,1,0);val.Position=UDim2.new(0,6,0,0);val.BackgroundTransparency=1;val.TextXAlignment=Enum.TextXAlignment.Left;val.TextColor3=UI.Text;val.Font=Enum.Font.Code;val.TextSize=11;val.Parent=btn
local arrow=Instance.new("TextLabel");arrow.Size=UDim2.new(0,14,1,0);arrow.Position=UDim2.new(1,-14,0,0);arrow.BackgroundTransparency=1;arrow.Text="▾";arrow.TextColor3=UI.Accent;arrow.Font=Enum.Font.Code;arrow.TextSize=11;arrow.Parent=btn
table.insert(AccentElements,arrow)
btn.MouseEnter:Connect(function() tweenUI(btn,{BackgroundColor3=UI.Hover}) end)
btn.MouseLeave:Connect(function() tweenUI(btn,{BackgroundColor3=UI.Panel2}) end)
local function Update() local v=GetFunc() val.Text=tostring(v~=nil and v or "") end
Update();registerComponent(Update)
btn.MouseButton1Click:Connect(function() openDropdown(btn,Options,function(opt) SetFunc(opt);Update() end) end)
end
Palette={Color3.fromRGB(124,110,255),Color3.fromRGB(255,255,255),Color3.fromRGB(50,205,50),Color3.fromRGB(0,150,255),Color3.fromRGB(255,255,0),Color3.fromRGB(255,0,255),Color3.fromRGB(0,255,255),Color3.fromRGB(255,128,0),Color3.fromRGB(255,45,85),Color3.fromRGB(90,143,255),Color3.fromRGB(0,0,0)}
function openRgbPicker(anchor,titleText,getColor,setColor)
local prevPop=ColorPopup;local prevCatch=ColorCatcher
if prevPop then prevPop.Visible=false end
if prevCatch then prevCatch.Visible=false end
ColorPopup=nil;ColorCatcher=nil
-- // [重写] 色板式选择器: 一堆颜色摆在一起, 点哪个用哪个 (旧版 R/G/B 滑块会被拦截层抢点击, 一滑就关) //
local colors={}
for _,c in ipairs(Palette) do table.insert(colors,c) end
local okc,curc=pcall(getColor)
if okc and curc and not table.find(colors,curc) then table.insert(colors,1,curc) end
local cols=5;local sw=36;local gap=8
local rows=math.ceil(#colors/cols)
local W=12+cols*sw+(cols-1)*gap+12
local H=32+rows*sw+(rows-1)*gap+12
local popup,catcher
local function closePicker()
if ColorPopup==popup then pcall(function() popup:Destroy() end) end
if catcher and ColorCatcher==catcher then pcall(function() catcher:Destroy() end) end
ColorPopup=prevPop;ColorCatcher=prevCatch
if prevPop then prevPop.Visible=true end
if prevCatch then prevCatch.Visible=true end
end
-- // [修复] 拦截层必须比弹窗先创建: GUI 命中测试按 Children 倒序, 后创建的先收到点击, 旧版点色块实际点到拦截层直接关面板 //
catcher=Instance.new('TextButton');catcher.Size=UDim2.new(1,0,1,0);catcher.BackgroundTransparency=1;catcher.Text='';catcher.ZIndex=95;catcher.AutoButtonColor=false;catcher.Parent=PopupParent
catcher.MouseButton1Click:Connect(closePicker)
popup=Instance.new('Frame');popup.Size=UDim2.new(0,W,0,H)
local ax=anchor.AbsolutePosition.X;local ay=anchor.AbsolutePosition.Y+anchor.AbsoluteSize.Y+4
popup.Position=UDim2.fromOffset(math.clamp(ax,4,Camera.ViewportSize.X-W-4),math.clamp(ay,4,Camera.ViewportSize.Y-H-4))
popup.BackgroundColor3=UI.BG;popup.BackgroundTransparency=curT();popup.BorderSizePixel=0;popup.ZIndex=100;popup.Parent=PopupParent;addStroke(popup,UI.Accent)
local title=Instance.new('TextLabel');title.Name='HateBold';title.Size=UDim2.new(1,-20,0,16);title.Position=UDim2.new(0,10,0,8);title.BackgroundTransparency=1;title.Text=titleText;title.TextColor3=UI.Text;title.Font=Enum.Font.GothamBold;title.TextSize=12;title.TextXAlignment=Enum.TextXAlignment.Left;title.ZIndex=101;title.Parent=popup
for i,c in ipairs(colors) do
local x=12+(i-1)%cols*(sw+gap)
local y=32+math.floor((i-1)/cols)*(sw+gap)
local s=Instance.new('TextButton');s.Size=UDim2.new(0,sw,0,sw);s.Position=UDim2.fromOffset(x,y);s.BackgroundColor3=c;s.BorderSizePixel=0;s.Text='';s.AutoButtonColor=false;s.ZIndex=101;s.Parent=popup
if i==1 and okc then addStroke(s,UI.Accent) end
s.MouseButton1Click:Connect(function() pcall(function() setColor(c) end) pcall(refreshAllComponents) closePicker() end)
end
ColorPopup=popup;ColorCatcher=catcher
end
function CreateColorPicker(parent,langKey,GetFunc,SetFunc)
local row=Instance.new("Frame");row.Size=UDim2.new(1,0,0,22);row.BackgroundTransparency=1;row.Parent=parent
local lbl=Instance.new("TextLabel");lbl.Size=UDim2.new(1,-74,1,0);lbl.Position=UDim2.new(0,5,0,0);lbl.BackgroundTransparency=1;lbl.TextXAlignment=Enum.TextXAlignment.Left;lbl.TextColor3=UI.TextDim;lbl.Font=UI_Font;lbl.TextSize=11;lbl.Parent=row;registerLang(lbl,langKey)
local cur=Instance.new("TextButton");cur.Size=UDim2.new(0,14,0,14);cur.Position=UDim2.new(1,-68,0.5,-7);cur.BackgroundColor3=GetFunc();cur.BorderSizePixel=0;cur.Text="";cur.AutoButtonColor=false;cur.Parent=row;addStroke(cur)
local btn=Instance.new("TextButton");btn.Size=UDim2.new(0,46,0,16);btn.Position=UDim2.new(1,-50,0.5,-8);btn.BackgroundColor3=UI.Panel2;btn.BorderSizePixel=0;btn.Text=T("ColorBtn");btn.TextColor3=UI.Text;btn.Font=UI_Font;btn.TextSize=10;btn.AutoButtonColor=false;btn.Parent=row;addStroke(btn)
btn.MouseEnter:Connect(function() tweenUI(btn,{BackgroundColor3=UI.Hover}) end)
btn.MouseLeave:Connect(function() tweenUI(btn,{BackgroundColor3=UI.Panel2}) end)
local function openPicker() openRgbPicker(btn,T(langKey),function() return GetFunc() end,function(c) SetFunc(c) end) end
btn.MouseButton1Click:Connect(openPicker)
cur.MouseButton1Click:Connect(openPicker)
local function Update() pcall(function() cur.BackgroundColor3=GetFunc() end) end
Update();registerComponent(Update)
pcall(function() GetFunc().Changed:Connect(Update) end)
end
AdvOpen={}
function CreateAdvanced(parent,langKey,buildFn)
local wrap=Instance.new("Frame");wrap.Size=UDim2.new(1,0,0,0);wrap.AutomaticSize=Enum.AutomaticSize.Y;wrap.BackgroundTransparency=1;wrap.Parent=parent
local wl=Instance.new("UIListLayout");wl.Padding=UDim.new(0,2);wl.Parent=wrap
local row=Instance.new("TextButton");row.Size=UDim2.new(1,0,0,18);row.BackgroundColor3=UI.Panel2;row.BorderSizePixel=0;row.Text="";row.AutoButtonColor=false;row.Parent=wrap;addStroke(row)
local lbl=Instance.new("TextLabel");lbl.Size=UDim2.new(1,-20,1,0);lbl.Position=UDim2.new(0,6,0,0);lbl.BackgroundTransparency=1;lbl.TextXAlignment=Enum.TextXAlignment.Left;lbl.TextColor3=UI.TextDim;lbl.Font=UI_Font;lbl.TextSize=11;lbl.Parent=row;registerLang(lbl,langKey)
local arrow=Instance.new("TextLabel");arrow.Size=UDim2.new(0,14,1,0);arrow.Position=UDim2.new(1,-16,0,0);arrow.BackgroundTransparency=1;arrow.Text="▸";arrow.TextColor3=UI.Accent;arrow.Font=Enum.Font.Code;arrow.TextSize=11;arrow.Parent=row
table.insert(AccentElements,arrow)
local body=Instance.new("Frame");body.Size=UDim2.new(1,0,0,0);body.AutomaticSize=Enum.AutomaticSize.Y;body.BackgroundTransparency=1;body.Visible=false;body.Parent=wrap
local bl=Instance.new("UIListLayout");bl.Padding=UDim.new(0,2);bl.Parent=body
local bp=Instance.new("UIPadding");bp.PaddingTop=UDim.new(0,2);bp.PaddingLeft=UDim.new(0,4);bp.PaddingRight=UDim.new(0,4);bp.PaddingBottom=UDim.new(0,2);bp.Parent=body
local open=false
local function set(v) open=v body.Visible=open arrow.Text=open and "▾" or "▸" end
if Config["UI Settings"] and Config["UI Settings"].AdvOpen and Config["UI Settings"].AdvOpen[langKey]==true then open=true end
buildFn(body)
set(open)
row.MouseEnter:Connect(function() tweenUI(row,{BackgroundColor3=UI.Hover}) end)
row.MouseLeave:Connect(function() tweenUI(row,{BackgroundColor3=UI.Panel2}) end)
row.MouseButton1Click:Connect(function()
set(not open)
if Config["UI Settings"] then if not Config["UI Settings"].AdvOpen then Config["UI Settings"].AdvOpen={} end Config["UI Settings"].AdvOpen[langKey]=open end
end)
return wrap,row
end
function CreateColorPopupButton(parent,langKey,entries)
local btn=Instance.new("TextButton");btn.Size=UDim2.new(1,0,0,22);btn.BackgroundColor3=UI.Panel2;btn.BorderSizePixel=0;btn.Text="";btn.AutoButtonColor=false;btn.Parent=parent;addStroke(btn)
local lbl=Instance.new("TextLabel");lbl.Size=UDim2.new(1,-24,1,0);lbl.Position=UDim2.new(0,6,0,0);lbl.BackgroundTransparency=1;lbl.TextXAlignment=Enum.TextXAlignment.Left;lbl.TextColor3=UI.Text;lbl.Font=UI_Font;lbl.TextSize=12;lbl.Parent=btn;registerLang(lbl,langKey)
local arrow=Instance.new("TextLabel");arrow.Size=UDim2.new(0,14,1,0);arrow.Position=UDim2.new(1,-16,0,0);arrow.BackgroundTransparency=1;arrow.Text="▸";arrow.TextColor3=UI.Accent;arrow.Font=Enum.Font.Code;arrow.TextSize=11;arrow.Parent=btn
table.insert(AccentElements,arrow)
btn.MouseEnter:Connect(function() tweenUI(btn,{BackgroundColor3=UI.Hover}) end)
btn.MouseLeave:Connect(function() tweenUI(btn,{BackgroundColor3=UI.Panel2}) end)
btn.MouseButton1Click:Connect(function()
closeColorPopup()
local catcher=Instance.new("TextButton");catcher.Size=UDim2.new(1,0,1,0);catcher.BackgroundTransparency=1;catcher.Text="";catcher.ZIndex=95;catcher.Parent=PopupParent
local pos=UserInputService:GetMouseLocation()
local h=34+#entries*24
local popup=Instance.new("Frame");popup.Size=UDim2.new(0,336,0,h)
popup.Position=UDim2.new(0,math.min(pos.X,Camera.ViewportSize.X-346),0,math.min(pos.Y,Camera.ViewportSize.Y-(h+10)))
popup.BackgroundColor3=UI.BG;popup.BackgroundTransparency=curT();popup.BorderSizePixel=0;popup.ZIndex=100;popup.Parent=PopupParent;addStroke(popup,UI.Accent)
local title=Instance.new("TextLabel");title.Name="HateBold";title.Size=UDim2.new(1,-16,0,22);title.Position=UDim2.new(0,8,0,4);title.BackgroundTransparency=1;title.Text=T(langKey);title.TextColor3=UI.Accent;title.Font=Enum.Font.GothamBold;title.TextSize=12;title.TextXAlignment=Enum.TextXAlignment.Left;title.ZIndex=101;title.Parent=popup
for i,entry in ipairs(entries) do
local r=Instance.new("Frame");r.Size=UDim2.new(1,-16,0,22);r.Position=UDim2.new(0,8,0,26+(i-1)*24);r.BackgroundTransparency=1;r.ZIndex=101;r.Parent=popup
local l=Instance.new("TextLabel");l.Size=UDim2.new(0,120,1,0);l.BackgroundTransparency=1;l.Font=UI_Font;l.TextSize=11;l.TextXAlignment=Enum.TextXAlignment.Left;l.TextColor3=UI.TextDim;l.Text=T(entry[1]);l.ZIndex=101;l.Parent=r
local chip=Instance.new("Frame");chip.Size=UDim2.new(0,14,0,14);chip.Position=UDim2.new(1,-102,0.5,-7);chip.BackgroundColor3=entry[2]();chip.BorderSizePixel=0;chip.ZIndex=101;chip.Parent=r;addStroke(chip,UI.Line)
local rb=Instance.new("TextButton");rb.Size=UDim2.new(0,46,0,16);rb.Position=UDim2.new(1,-84,0.5,-8);rb.BackgroundColor3=UI.Panel2;rb.BorderSizePixel=0;rb.Text=T("ColorBtn");rb.TextColor3=UI.Text;rb.Font=UI_Font;rb.TextSize=10;rb.AutoButtonColor=false;rb.ZIndex=102;rb.Parent=r;addStroke(rb)
rb.MouseButton1Click:Connect(function() openRgbPicker(rb,T(entry[1]),function() return entry[2]() end,function(c) entry[3](c) end) end)
local function Upd() pcall(function() chip.BackgroundColor3=entry[2]() end) end
Upd()
end
catcher.MouseButton1Click:Connect(closeColorPopup)
ColorPopup=popup;ColorCatcher=catcher
end)
return btn
end
function CreateButton(parent,langKey,cb)
local row=Instance.new("TextButton");row.Size=UDim2.new(1,0,0,22);row.BackgroundColor3=UI.Panel2;row.BorderSizePixel=0;row.Text="";row.AutoButtonColor=false;row.Parent=parent;addStroke(row)
local lbl=Instance.new("TextLabel");lbl.Size=UDim2.new(1,-24,1,0);lbl.Position=UDim2.new(0,6,0,0);lbl.BackgroundTransparency=1;lbl.TextXAlignment=Enum.TextXAlignment.Left;lbl.TextColor3=UI.Text;lbl.Font=UI_Font;lbl.TextSize=12;lbl.Parent=row;registerLang(lbl,langKey)
local arrow=Instance.new("TextLabel");arrow.Size=UDim2.new(0,14,1,0);arrow.Position=UDim2.new(1,-16,0,0);arrow.BackgroundTransparency=1;arrow.Text="▸";arrow.TextColor3=UI.Accent;arrow.Font=Enum.Font.Code;arrow.TextSize=11;arrow.Parent=row
table.insert(AccentElements,arrow)
row.MouseEnter:Connect(function() tweenUI(row,{BackgroundColor3=UI.Hover}) end)
row.MouseLeave:Connect(function() tweenUI(row,{BackgroundColor3=UI.Panel2}) end)
row.MouseButton1Click:Connect(cb)
return row
end
function openGridPopup(title,cats,multi,cur,onSingle,onConfirm)
closeGridPopup()
cats=cats or {}
-- // [重写] 弹窗三件套: 独立顶层 Gui + 先登记后构建 + 手动排版(不用 UIGridLayout/AutomaticSize/UIListLayout) //
-- // 之前一旦构建中途报错, 全屏拦截层就永远留在屏幕上 -> 空白 + 点不动 + 整个 UI 卡死 //
local W=460;local H=460
local c=Instance.new("TextButton");c.Size=UDim2.new(1,0,1,0);c.BackgroundTransparency=1;c.Text="";c.ZIndex=10;c.AutoButtonColor=false;c.Parent=PopupParent
local f=Instance.new("Frame");f.Size=UDim2.new(0,W,0,H);f.AnchorPoint=Vector2.new(0.5,0.5);f.Position=UDim2.new(0.5,0,0.5,0);f.BackgroundColor3=UI.BG;f.BackgroundTransparency=0;f.BorderSizePixel=0;f.ZIndex=11;f.Active=true;f.ClipsDescendants=true;f.Parent=PopupParent
GridPopup={f=f,c=c}
local sel={}
if multi and cur and type(cur)=="table" then for k,v in pairs(cur) do sel[k]=v end end
local openedAt=tick()
local ok,err=pcall(function()
addStroke(f,UI.Accent)
local fTop=Instance.new("Frame");fTop.Size=UDim2.new(1,0,0,30);fTop.BackgroundColor3=UI.Top;fTop.BorderSizePixel=0;fTop.ZIndex=12;fTop.Parent=f
local tl=Instance.new("TextLabel");tl.Name="HateBold";tl.Size=UDim2.new(1,-72,1,0);tl.Position=UDim2.new(0,8,0,0);tl.BackgroundTransparency=1;tl.Text=tostring(title);tl.TextColor3=UI.Accent;tl.Font=Enum.Font.GothamBold;tl.TextSize=13;tl.TextXAlignment=Enum.TextXAlignment.Left;tl.ZIndex=13;tl.Parent=fTop
local closeB=Instance.new("TextButton");closeB.Size=UDim2.new(0,58,0,20);closeB.Position=UDim2.new(1,-66,0,5);closeB.BackgroundColor3=UI.Panel2;closeB.Text=T("Cancel");closeB.TextColor3=UI.Danger;closeB.Font=UI_Font;closeB.TextSize=11;closeB.AutoButtonColor=false;closeB.ZIndex=13;closeB.Parent=fTop;addStroke(closeB)
closeB.MouseButton1Click:Connect(closeGridPopup)
local tabBar=Instance.new("Frame");tabBar.Size=UDim2.new(1,-16,0,24);tabBar.Position=UDim2.new(0,8,0,36);tabBar.BackgroundTransparency=1;tabBar.ZIndex=12;tabBar.ClipsDescendants=true;tabBar.Parent=f
local hint=Instance.new("TextLabel");hint.Size=UDim2.new(1,-16,0,16);hint.Position=UDim2.new(0,8,1,-22);hint.BackgroundTransparency=1;hint.Text=multi and T("GridHintMulti") or T("GridHintSingle");hint.TextColor3=UI.TextDim;hint.Font=UI_Font;hint.TextSize=9;hint.TextXAlignment=Enum.TextXAlignment.Left;hint.ZIndex=12;hint.Parent=f
local bottomH=26
if multi then
bottomH=56
local confirmB=Instance.new("TextButton");confirmB.Size=UDim2.new(1,-16,0,24);confirmB.Position=UDim2.new(0,8,1,-52);confirmB.BackgroundColor3=UI.Accent;confirmB.Text=T("Save");confirmB.TextColor3=Color3.new(0,0,0);confirmB.Font=UI_Font;confirmB.TextSize=12;confirmB.AutoButtonColor=false;confirmB.ZIndex=13;confirmB.Parent=f
confirmB.MouseButton1Click:Connect(function() local fn=onConfirm local s={} for k,v in pairs(sel) do s[k]=v end closeGridPopup() if fn then pcall(fn,s) end end)
end
local scroll=Instance.new("ScrollingFrame");scroll.Size=UDim2.new(1,-16,0,H-68-bottomH);scroll.Position=UDim2.new(0,8,0,64);scroll.BackgroundTransparency=1;scroll.BorderSizePixel=0;scroll.ScrollBarThickness=4;scroll.AutomaticCanvasSize=Enum.AutomaticSize.None;scroll.CanvasSize=UDim2.new(0,0,0,0);scroll.ScrollBarImageColor3=UI.Accent;scroll.ScrollingDirection=Enum.ScrollingDirection.Y;scroll.ZIndex=12;scroll.Parent=f;scroll.Active=true
local colW=212;local rowH=28;local pad=6
local function clearList() for _,ch in ipairs(scroll:GetChildren()) do if ch:IsA("GuiObject") then ch:Destroy() end end end
local function msg(text,col)
clearList()
local e=Instance.new("TextLabel");e.Size=UDim2.new(1,-12,0,120);e.Position=UDim2.new(0,6,0,24);e.BackgroundTransparency=1;e.Text=tostring(text);e.TextColor3=col or UI.TextDim;e.Font=UI_Font;e.TextSize=12;e.TextXAlignment=Enum.TextXAlignment.Center;e.TextWrapped=true;e.ZIndex=13;e.Parent=scroll
scroll.CanvasSize=UDim2.new(0,0,0,150)
end
local function populate(cat)
local items=(cat and cat.items) or {}
clearList()
if #items==0 then msg(T("GridEmpty"),UI.Danger) return end
for idx,item in ipairs(items) do
local b=Instance.new("TextButton");b.Size=UDim2.new(0,colW,0,24);b.Position=UDim2.new(0,pad+((idx-1)%2)*(colW+4),0,math.floor((idx-1)/2)*rowH);b.BackgroundColor3=UI.Panel2;b.BorderSizePixel=0;b.ZIndex=13;b.AutoButtonColor=false;b.Parent=scroll
pcall(function() b.TextTruncate=Enum.TextTruncate.AtEnd end)
local st=Instance.new("UIStroke");st.Color=UI.Stroke;st.Thickness=1;st.Parent=b
local function look()
local on=multi and sel[item]
b.Text="  "..tostring(itemDisplay(item))..((multi and on) and "  [v]" or "")
b.TextColor3=(on and UI.Accent) or UI.Text
b.TextSize=11;b.Font=UI_Font;b.TextXAlignment=Enum.TextXAlignment.Left
if on then st.Color=UI.Accent b.BackgroundColor3=UI.Hover else st.Color=UI.Stroke b.BackgroundColor3=UI.Panel2 end
end
look()
b.MouseEnter:Connect(function() st.Color=UI.Accent end)
b.MouseLeave:Connect(function() look() end)
b.MouseButton1Click:Connect(function()
if multi then sel[item]=(not sel[item]) or nil look()
else local fn=onSingle local it=item closeGridPopup() if fn then pcall(fn,it) end end
end)
b.MouseButton2Click:Connect(function() if multi then sel[item]=nil look() end end)
end
scroll.CanvasSize=UDim2.new(0,0,0,math.ceil(#items/2)*rowH+pad*2)
end
if #cats==0 then
msg(T("GridEmpty"),UI.Danger)
else
for i,cat in ipairs(cats) do
local tb=Instance.new("TextButton");tb.Size=UDim2.new(0,110,1,0);tb.Position=UDim2.new(0,(i-1)*114,0,0);tb.BackgroundColor3=UI.Panel2;tb.BorderSizePixel=0;tb.Text=tostring(cat.name);tb.TextColor3=UI.Text;tb.Font=UI_Font;tb.TextSize=11;tb.AutoButtonColor=false;tb.ZIndex=13;tb.Parent=tabBar
pcall(function() tb.TextTruncate=Enum.TextTruncate.AtEnd end)
local tSt=Instance.new("UIStroke");tSt.Color=UI.Stroke;tSt.Thickness=1;tSt.Parent=tb
local function pick()
for _,o in ipairs(tabBar:GetChildren()) do if o:IsA("TextButton") then o.BackgroundColor3=UI.Panel2 local s2=o:FindFirstChildOfClass("UIStroke") if s2 then s2.Color=UI.Stroke end end end
tb.BackgroundColor3=UI.Accent tSt.Color=UI.Accent
local pok,pe=pcall(populate,cat) if not pok then msg(pe,UI.Danger) end
end
tb.MouseButton1Click:Connect(pick)
if i==1 then pick() end
end
end
end)
if not ok then
-- // 构建失败也必须能关掉, 并把错误显示出来, 绝不让拦截层卡死整个 UI //
pcall(function()
local e=Instance.new("TextLabel");e.Size=UDim2.new(1,-16,0,300);e.Position=UDim2.new(0,8,0,56);e.BackgroundTransparency=1;e.Text="Popup build error:\n"..tostring(err);e.TextColor3=UI.Danger;e.Font=Enum.Font.Code;e.TextSize=11;e.TextWrapped=true;e.TextXAlignment=Enum.TextXAlignment.Left;e.ZIndex=30;e.Parent=f
local cb=Instance.new("TextButton");cb.Size=UDim2.new(1,-16,0,28);cb.Position=UDim2.new(0,8,1,-32);cb.BackgroundColor3=UI.Danger;cb.Text=T("Cancel");cb.TextColor3=Color3.new(1,1,1);cb.Font=UI_Font;cb.TextSize=11;cb.AutoButtonColor=false;cb.ZIndex=30;cb.Parent=f
cb.MouseButton1Click:Connect(closeGridPopup)
end)
return f
end
c.MouseButton1Click:Connect(function() if tick()-openedAt>0.2 then closeGridPopup() end end)
local conn
conn=UserInputService.InputBegan:Connect(function(input,gpe)
if gpe then return end
if input.KeyCode==Enum.KeyCode.Escape then closeGridPopup() end
end)
GridPopup.conn=conn
return f
end
function CreateWeaponBox(parent,langKey,GetFunc,SetFunc)
local row=Instance.new("Frame");row.Size=UDim2.new(1,0,0,40);row.BackgroundTransparency=1;row.Parent=parent
local lbl=Instance.new("TextLabel");lbl.Size=UDim2.new(1,0,0,14);lbl.Position=UDim2.new(0,5,0,0);lbl.BackgroundTransparency=1;lbl.TextColor3=UI.TextDim;lbl.Font=UI_Font;lbl.TextSize=10;lbl.TextXAlignment=Enum.TextXAlignment.Left;lbl.Parent=row;registerLang(lbl,langKey)
local box=Instance.new("TextBox");box.Size=UDim2.new(1,0,0,18);box.Position=UDim2.new(0,0,1,-18)
box.BackgroundColor3=UI.Panel2;box.BorderSizePixel=0;box.Text=table.concat(GetFunc(),", ")
box.PlaceholderText="[Weapon1], [Weapon2]";box.TextColor3=UI.Text;box.PlaceholderColor3=UI.TextDim
box.Font=Enum.Font.Code;box.TextSize=11;box.ClearTextOnFocus=false;box.Parent=row;addStroke(box)
box.Focused:Connect(function() pcall(function() box:FindFirstChildOfClass("UIStroke").Color=UI.Accent end) end)
box.FocusLost:Connect(function()
pcall(function() box:FindFirstChildOfClass("UIStroke").Color=UI.Stroke end)
local parts={}
for w in box.Text:gmatch("[^,]+") do w=w:match("^%s*(.-)%s*$") if w~="" then table.insert(parts,w) end end
SetFunc(parts);box.Text=table.concat(parts,", ")
end)
end
function CreateTextBox(parent,langKey,placeholder,GetFunc,SetFunc)
local row=Instance.new("Frame");row.Size=UDim2.new(1,0,0,24);row.BackgroundTransparency=1;row.Parent=parent
local lbl=Instance.new("TextLabel");lbl.Size=UDim2.new(0.4,-6,1,0);lbl.Position=UDim2.new(0,5,0,0);lbl.BackgroundTransparency=1;lbl.TextXAlignment=Enum.TextXAlignment.Left;lbl.TextColor3=UI.TextDim;lbl.Font=UI_Font;lbl.TextSize=12;lbl.Parent=row;registerLang(lbl,langKey)
local box=Instance.new("TextBox");box.Size=UDim2.new(0.6,-5,0,18);box.Position=UDim2.new(0.4,0,0.5,-9);box.BackgroundColor3=UI.Panel2;box.BorderSizePixel=0;box.Text=GetFunc() or "";box.PlaceholderText=placeholder;box.TextColor3=UI.Text;box.PlaceholderColor3=UI.TextDim;box.Font=Enum.Font.Code;box.TextSize=11;box.ClearTextOnFocus=false;box.Parent=row;addStroke(box)
box.FocusLost:Connect(function() SetFunc(box.Text) end)
return row,box
end
function showKeybindPopup(bindTable,pos)
if type(bindTable)~="table" then bindTable={Key=''} end
if KeybindPopup then pcall(function() KeybindPopup:Destroy() end);KeybindPopup=nil end
WaitingForKey=nil
local popup=Instance.new("Frame")
popup.Size=UDim2.new(0,226,0,150)
popup.Position=UDim2.new(0,math.min(pos.X,Camera.ViewportSize.X-236),0,math.min(pos.Y,Camera.ViewportSize.Y-166))
popup.BackgroundColor3=UI.BG;popup.BackgroundTransparency=curT();popup.BorderSizePixel=0;popup.ZIndex=100;popup.Parent=PopupParent
addStroke(popup,UI.Accent)
local title=Instance.new("TextLabel");title.Name="HateBold";title.Size=UDim2.new(1,-16,0,24);title.Position=UDim2.new(0,8,0,6);title.BackgroundTransparency=1;title.Text=T("Keybind");title.TextColor3=UI.Accent;title.Font=Enum.Font.GothamBold;title.TextSize=13;title.TextXAlignment=Enum.TextXAlignment.Left;title.ZIndex=101;title.Parent=popup
local keyBtn=Instance.new("TextButton");keyBtn.Size=UDim2.new(1,-16,0,28);keyBtn.Position=UDim2.new(0,8,0,34)
keyBtn.BackgroundColor3=UI.Panel2;keyBtn.BorderSizePixel=0
keyBtn.Text=(bindTable.Key=='' or not bindTable.Key) and T("None") or tostring(bindTable.Key)
keyBtn.TextColor3=UI.Text;keyBtn.Font=Enum.Font.Code;keyBtn.TextSize=12;keyBtn.ZIndex=101;keyBtn.Parent=popup
addStroke(keyBtn)
keyBtn.MouseEnter:Connect(function() tweenUI(keyBtn,{BackgroundColor3=UI.Hover}) end)
keyBtn.MouseLeave:Connect(function() tweenUI(keyBtn,{BackgroundColor3=UI.Panel2}) end)
keyBtn.MouseButton1Click:Connect(function() WaitingForKey={bindTable=bindTable,btn=keyBtn};keyBtn.Text=T("PressKey") end)
local yOff=68
if bindTable.Mode~=nil then
local modeBtn=Instance.new("TextButton");modeBtn.Size=UDim2.new(0.5,-12,0,26);modeBtn.Position=UDim2.new(0,8,0,yOff)
modeBtn.BackgroundColor3=UI.Panel2;modeBtn.BorderSizePixel=0;modeBtn.Text=(bindTable.Mode=='Hold') and T("ModeHold") or T("ModeToggle");modeBtn.TextColor3=UI.Accent;modeBtn.Font=UI_Font;modeBtn.TextSize=11;modeBtn.ZIndex=101;modeBtn.Parent=popup
addStroke(modeBtn)
modeBtn.MouseButton1Click:Connect(function() bindTable.Mode=(bindTable.Mode=='Toggle') and 'Hold' or 'Toggle';modeBtn.Text=(bindTable.Mode=='Hold') and T("ModeHold") or T("ModeToggle");updateKeybindDisplay() end)
local clearBtn=Instance.new("TextButton");clearBtn.Size=UDim2.new(0.5,-12,0,26);clearBtn.Position=UDim2.new(0.5,4,0,yOff)
clearBtn.BackgroundColor3=UI.Panel2;clearBtn.BorderSizePixel=0;clearBtn.Text=T("Clear");clearBtn.TextColor3=UI.Danger;clearBtn.Font=UI_Font;clearBtn.TextSize=11;clearBtn.ZIndex=101;clearBtn.Parent=popup
addStroke(clearBtn)
clearBtn.MouseButton1Click:Connect(function() bindTable.Key='';WaitingForKey=nil;popup:Destroy();KeybindPopup=nil;refreshAllComponents();updateKeybindDisplay() end)
else
local clearBtn=Instance.new("TextButton");clearBtn.Size=UDim2.new(1,-16,0,26);clearBtn.Position=UDim2.new(0,8,0,yOff)
clearBtn.BackgroundColor3=UI.Panel2;clearBtn.BorderSizePixel=0;clearBtn.Text=T("Clear");clearBtn.TextColor3=UI.Danger;clearBtn.Font=UI_Font;clearBtn.TextSize=11;clearBtn.ZIndex=101;clearBtn.Parent=popup
addStroke(clearBtn)
clearBtn.MouseButton1Click:Connect(function() bindTable.Key='';WaitingForKey=nil;popup:Destroy();KeybindPopup=nil;refreshAllComponents();updateKeybindDisplay() end)
end
yOff=yOff+32
local cancelBtn=Instance.new("TextButton");cancelBtn.Size=UDim2.new(1,-16,0,26);cancelBtn.Position=UDim2.new(0,8,0,yOff)
cancelBtn.BackgroundColor3=UI.Panel2;cancelBtn.BorderSizePixel=0;cancelBtn.Text=T("Cancel");cancelBtn.TextColor3=UI.TextDim;cancelBtn.Font=UI_Font;cancelBtn.TextSize=11;cancelBtn.ZIndex=101;cancelBtn.Parent=popup
cancelBtn.MouseButton1Click:Connect(function() WaitingForKey=nil;popup:Destroy();KeybindPopup=nil end)
popup.Size=UDim2.new(0,226,0,yOff+34)
KeybindPopup=popup
end
function attachKeybind(btn,bindTable)
btn.MouseButton2Click:Connect(function() showKeybindPopup(bindTable,UserInputService:GetMouseLocation()) end)
local lbl=btn:FindFirstChildOfClass("TextLabel")
if lbl and not BindSuffixSet[lbl] then
BindSuffixSet[lbl]=true
lbl.Text=lbl.Text.." ("..T("BindKey")..")"
end
end
function CreateKeybindRow(parent,langKey,bindTable)
if type(bindTable)~="table" then bindTable={Key=''} end
local row=Instance.new("TextButton");row.Size=UDim2.new(1,0,0,22);row.BackgroundColor3=UI.Hover;row.BackgroundTransparency=1;row.Text="";row.AutoButtonColor=false;row.BorderSizePixel=0;row.Parent=parent
local lbl=Instance.new("TextLabel");lbl.Size=UDim2.new(1,-96,1,0);lbl.Position=UDim2.new(0,5,0,0);lbl.BackgroundTransparency=1;lbl.TextColor3=UI.TextDim;lbl.Font=UI_Font;lbl.TextSize=12;lbl.TextXAlignment=Enum.TextXAlignment.Left;lbl.Parent=row;registerLang(lbl,langKey)
local keyBtn=Instance.new("TextButton");keyBtn.Size=UDim2.new(0,84,0,18);keyBtn.AnchorPoint=Vector2.new(1,0.5);keyBtn.Position=UDim2.new(1,-5,0.5,0);keyBtn.BackgroundColor3=UI.Panel2;keyBtn.BorderSizePixel=0;keyBtn.Font=Enum.Font.Code;keyBtn.TextSize=11;keyBtn.AutoButtonColor=false;keyBtn.Parent=row;addStroke(keyBtn)
local function Update() local k=bindTable and bindTable.Key or '';keyBtn.Text=(k=='' or not k) and T("None") or tostring(k);keyBtn.TextColor3=(k=='' or not k) and UI.TextDim or UI.Accent end
Update();registerComponent(Update)
row.MouseEnter:Connect(function() tweenUI(row,{BackgroundTransparency=0.8}) end)
row.MouseLeave:Connect(function() tweenUI(row,{BackgroundTransparency=1}) end)
row.MouseButton1Click:Connect(function() showKeybindPopup(bindTable,UserInputService:GetMouseLocation()) end)
end
track(UserInputService.InputBegan:Connect(function(input)
if WaitingForKey and not isTyping() then
if input.KeyCode==Enum.KeyCode.Escape then WaitingForKey=nil;if KeybindPopup then pcall(function() KeybindPopup:Destroy() end) KeybindPopup=nil end return end
local keyName=nil
if input.UserInputType==Enum.UserInputType.Keyboard then keyName=input.KeyCode.Name
elseif string.find(input.UserInputType.Name,"MouseButton") then keyName=input.UserInputType.Name end
if keyName then
WaitingForKey.bindTable.Key=keyName;WaitingForKey=nil;BindConsumed=true
task.delay(0.1,function() BindConsumed=false end)
if KeybindPopup then pcall(function() KeybindPopup:Destroy() end) KeybindPopup=nil end
refreshAllComponents();updateKeybindDisplay()
end
end
end))
function UnloadScript()
Unloaded=true
if rainbowConn then pcall(function() rainbowConn:Disconnect() end) rainbowConn=nil end
local hum=LocalPlayer.Character and LocalPlayer.Character:FindFirstChildOfClass("Humanoid")
if hum then hum.WalkSpeed=16;hum.AutoRotate=true end
if emoteTrack then pcall(function() emoteTrack:Stop() end) emoteTrack=nil end
if animSpamTrack then pcall(function() animSpamTrack:Stop() end) animSpamTrack=nil end
pcall(function() setreadonly(grm,false);grm.__index=oldIndex;if oldNamecall~=nil then grm.__namecall=oldNamecall end;grm.__newindex=oldNewindex;setreadonly(grm,true) end)
pcall(function() math.random=originalRandom end)
for _,conn in pairs(AllConnections) do pcall(function() conn:Disconnect() end) end
for _,esp in pairs(espLabels) do pcall(function() esp.nameTag:Remove() esp.line:Remove() esp.box:Remove() esp.boxO:Remove() esp.fill:Remove() esp.weaponTag:Remove() esp.distTag:Remove() esp.healthBG:Remove() esp.healthFG:Remove() esp.healthText:Remove() esp.armorBar:Remove() for _,l in pairs(esp.skeleton) do l:Remove() end end) pcall(function() if esp.chams then esp.chams:Destroy() end end) end
espLabels={}
for _,o in pairs(keybindDisplayObjects) do pcall(function() o:Remove() end) end
for _,l in pairs(viewLines) do pcall(function() l:Remove() end) end
viewLines={}
for i=1,4 do pcall(function() crossLines[i].l:Remove();crossLines[i].o:Remove() end) end
for _,n in ipairs(notifications) do pcall(function() n.t:Remove() end) pcall(function() n.ttl:Remove() end) pcall(function() n.bg:Remove() end) pcall(function() n.edge:Remove() end) end
for _,x in ipairs(toastLines) do pcall(function() x.t:Remove() end) end
pcall(function() fovCircle:Remove() end);pcall(function() aaFovCircle:Remove() end);pcall(function() lockLine:Remove() end);pcall(function() stickyFov:Remove() end);pcall(function() stickyTracer:Remove() end)
pcall(function() watermarkText:Remove() end)
pcall(function() particlePart:Destroy() end)
pcall(function() if auraAtt then auraAtt:Destroy() end end)
pcall(function() if desyncModel then desyncModel:Destroy() end end)
pcall(function() if trailObj then trailObj:Destroy() end end)
pcall(function() for _,c in pairs(Workspace:GetChildren()) do if c.Name=="\0" then c:Destroy() end end end)
pcall(function() for _,v in pairs(Workspace:GetDescendants()) do if v.Name=="HateTracer" or v.Name=="HateA" or v.Name=="HateImpact" then v:Destroy() end end end)
pcall(function() for _,v in pairs(Workspace.Terrain:GetChildren()) do if v.Name=="HateTracer" or v.Name=="HateA" then v:Destroy() end end end)
pcall(function() LocalPlayer.CameraMaxZoomDistance=origZoom end)
pcall(function() UserInputService.MouseIconEnabled=true end)
pcall(function() Lighting.Brightness=origLighting.Brightness;Lighting.FogEnd=origLighting.FogEnd;Lighting.ClockTime=origLighting.ClockTime;colorCorr.Saturation=origLighting.Saturation end)
pcall(function() sky.SkyboxBk=origSky.Bk;sky.SkyboxDn=origSky.Dn;sky.SkyboxFt=origSky.Ft;sky.SkyboxLf=origSky.Lf;sky.SkyboxRt=origSky.Rt;sky.SkyboxUp=origSky.Up end)
pcall(function() closeGridPopup() end)
pcall(function() if PopupGui then PopupGui:Destroy() end end);pcall(function() ScreenGui:Destroy() end);pcall(function() hudGui:Destroy() end)
if type(cleardrawcache)=="function" then pcall(cleardrawcache) end
pcall(function() if camFov then camFov:Remove() end end)
pcall(function() if desyncEye then desyncEye:Remove() end end)
pcall(desyncRestoreView)
pcall(function() RunService:UnbindFromRenderStep("HateCC_AimApply") end)
pcall(function() if desyncSetback then desyncSetback:Destroy() end end)
pcall(function() if auraPart then auraPart:Destroy() end end)
pcall(function() restoreForcefieldVisuals() end)
genv.__HateCC_Loaded=false;genv.__HateCC_Unload=nil
end
genv.__HateCC_Unload=UnloadScript
do
Launcher=Instance.new("Frame");Launcher.Size=UDim2.new(0,470,0,300);Launcher.Position=UDim2.new(0.5,-235,0.5,-142)
Launcher.BackgroundColor3=UI.BG;Launcher.BorderSizePixel=0;Launcher.Visible=true;Launcher.BackgroundTransparency=1;Launcher.Parent=ScreenGui
local lAcc=Instance.new("Frame");lAcc.Size=UDim2.new(1,0,0,2);lAcc.BackgroundColor3=UI.Accent;lAcc.BorderSizePixel=0;lAcc.Parent=Launcher;table.insert(AccentElements,lAcc)
addStroke(Launcher,UI.Accent)
local lTop=Instance.new("Frame");lTop.Size=UDim2.new(1,0,0,30);lTop.BackgroundColor3=UI.Top;lTop.BorderSizePixel=0;lTop.Parent=Launcher
local lLine=Instance.new("Frame");lLine.Size=UDim2.new(1,0,0,1);lLine.Position=UDim2.new(0,0,1,-1);lLine.BackgroundColor3=UI.Line;lLine.BorderSizePixel=0;lLine.Parent=lTop
local lTitle=Instance.new("TextLabel");lTitle.Name="HateBold";lTitle.Size=UDim2.new(1,-20,1,0);lTitle.Position=UDim2.new(0,10,0,0)
lTitle.BackgroundTransparency=1;lTitle.RichText=true;lTitle.Font=Enum.Font.GothamBold;lTitle.TextSize=14;lTitle.TextXAlignment=Enum.TextXAlignment.Left
lTitle.Text='<font color="rgb(124,110,255)">hate</font><font color="rgb(205,205,205)">.CC</font><font color="rgb(60,60,60)">  /  </font><font color="rgb(109,109,109)">da hood</font>';lTitle.Parent=lTop
local lVer=Instance.new("TextLabel");lVer.Size=UDim2.new(0,120,1,0);lVer.Position=UDim2.new(1,-130,0,0)
lVer.BackgroundTransparency=1;lVer.Font=Enum.Font.Code;lVer.TextSize=10;lVer.TextXAlignment=Enum.TextXAlignment.Right;lVer.TextColor3=UI.TextDim;lVer.Text="hate.CC";lVer.Parent=lTop
local lSide=Instance.new("Frame");lSide.Size=UDim2.new(0,92,1,-30);lSide.Position=UDim2.new(0,0,0,30);lSide.BackgroundColor3=UI.Sidebar;lSide.BorderSizePixel=0;lSide.Parent=Launcher
local lSideLine=Instance.new("Frame");lSideLine.Size=UDim2.new(0,1,1,0);lSideLine.Position=UDim2.new(1,-1,0,0);lSideLine.BackgroundColor3=UI.Line;lSideLine.BorderSizePixel=0;lSideLine.Parent=lSide
local lBig=Instance.new("TextLabel");lBig.Name="HateBold";lBig.Size=UDim2.new(1,0,0,34);lBig.Position=UDim2.new(0,0,0,16);lBig.BackgroundTransparency=1;lBig.Text="hate.CC";lBig.TextColor3=UI.Accent;lBig.Font=Enum.Font.GothamBlack;lBig.TextSize=16;lBig.Parent=lSide
table.insert(AccentElements,lBig)
local lRight=Instance.new("Frame");lRight.Size=UDim2.new(1,-108,1,-40);lRight.Position=UDim2.new(0,108,0,40);lRight.BackgroundColor3=UI.Panel;lRight.BorderSizePixel=0;lRight.Parent=Launcher;addStroke(lRight)
local lHint=Instance.new("TextLabel");lHint.Size=UDim2.new(1,-24,0,14);lHint.Position=UDim2.new(0,12,0,10);lHint.BackgroundTransparency=1;lHint.Text="hate.CC  |  da hood";lHint.TextColor3=UI.TextDim;lHint.Font=UI_Font;lHint.TextSize=11;lHint.TextXAlignment=Enum.TextXAlignment.Left;lHint.Parent=lRight
local function launcherButton(langKey,y,accent,cb)
local btn=Instance.new("TextButton");btn.Size=UDim2.new(1,-24,0,26);btn.Position=UDim2.new(0,12,0,y)
btn.BackgroundColor3=accent and UI.Accent or UI.Panel2;btn.BorderSizePixel=0;btn.Font=UI_Font;btn.TextSize=11;btn.AutoButtonColor=false
btn.TextColor3=accent and Color3.new(0,0,0) or UI.TextDim;btn.Parent=lRight
addStroke(btn,accent and UI.Accent or UI.Stroke)
registerLang(btn,langKey)
btn.MouseEnter:Connect(function() tweenUI(btn,{BackgroundColor3=accent and UI.Hover or UI.Hover}) end)
btn.MouseLeave:Connect(function() tweenUI(btn,{BackgroundColor3=accent and UI.Accent or UI.Panel2}) end)
btn.MouseButton1Click:Connect(cb)
end
local function doStart() Started=true;Launcher.Visible=false;openMenu();updateKeybindDisplay() end
launcherButton("Start",38,true,doStart)
launcherButton("Exit",70,false,function() UnloadScript() end)
task.delay(0.05,function()
tweenUI(Launcher,{BackgroundTransparency=0,Position=UDim2.new(0.5,-235,0.5,-150)},0.3)
end)
end
-- // UI BUILD //
do
local VA=Config['Visual Awareness']
local stBox=CreateSection(Pages.Aim.L,"StickyAim")
local stBtn=CreateToggle(stBox,"StickyAim",function() return Config['Sticky'].Enabled end,function(v) Config['Sticky'].Enabled=v;if not v then stickyLocked=false;stickyTargetPlayer=nil;currentTarget=nil end end)
attachKeybind(stBtn,Config.Keybinds['Target Lock'])
CreateDropdown(stBox,"HitPart",{"Head","UpperTorso","HumanoidRootPart","LowerTorso","Closest Part"},function() return Config['Sticky'].HitPart end,function(v) Config['Sticky'].HitPart=v end)
CreateDropdown(stBox,"StickyFire",{"Auto","Manual"},function() return Config['Sticky'].AutoFire and "Auto" or "Manual" end,function(v) Config['Sticky'].AutoFire=(v=="Auto") end)
CreateSlider(stBox,"StickyFireDelay",30,1000,function() return math.floor((Config['Sticky'].FireDelay or 0.12)*1000) end,function(v) Config['Sticky'].FireDelay=v/1000 end)
CreateToggle(stBox,"StickySpectate",function() return Config['Sticky'].Spectate end,function(v) Config['Sticky'].Spectate=v end)
CreateToggle(stBox,"StickyStomp",function() return Config['Sticky'].StompTarget end,function(v) Config['Sticky'].StompTarget=v end)
CreateToggle(stBox,"StickyInvBullets",function() return Config['Sticky'].InvisibleBullets end,function(v) Config['Sticky'].InvisibleBullets=v end)
CreateToggle(stBox,"StickyTracer",function() return Config['Sticky'].Tracer end,function(v) Config['Sticky'].Tracer=v end)
CreateDropdown(stBox,"StickyTracerMode",{"Mouse","HumanoidRootPart"},function() return Config['Sticky'].TracerMode end,function(v) Config['Sticky'].TracerMode=v end)
CreateColorPicker(stBox,"StickyTracerColor",function() return Config['Sticky'].TracerColor end,function(v) Config['Sticky'].TracerColor=v end)
CreateToggle(stBox,"StickyFOV",function() return Config['Sticky'].FOVEnabled end,function(v) Config['Sticky'].FOVEnabled=v end)
CreateSlider(stBox,"StickyFOVSize",50,1000,function() return Config['Sticky'].FOVSize end,function(v) Config['Sticky'].FOVSize=v end)
CreateColorPicker(stBox,"StickyFOVColor",function() return Config['Sticky'].FOVColor end,function(v) Config['Sticky'].FOVColor=v end)
CreateToggle(stBox,"StickyStrafe",function() return Config['Sticky'].Strafe end,function(v) Config['Sticky'].Strafe=v end)
CreateDropdown(stBox,"StickyStrafeMode",{"Orbit","Random"},function() return Config['Sticky'].StrafeMode end,function(v) Config['Sticky'].StrafeMode=v end)
CreateSlider(stBox,"StickyStrafeSpeed",1,20,function() return Config['Sticky'].StrafeSpeed end,function(v) Config['Sticky'].StrafeSpeed=v end)
CreateSlider(stBox,"StickyStrafeOffset",1,20,function() return Config['Sticky'].StrafeXOffset end,function(v) Config['Sticky'].StrafeXOffset=v end)
CreateToggle(stBox,"StickySpectateStrafe",function() return Config['Sticky'].SpectateStrafe end,function(v) Config['Sticky'].SpectateStrafe=v end)
WEAPONS={'[Revolver]','[Deagle]','[Glock]','[Silencer]','[Double-Barrel SG]','[TacticalShotgun]','[Shotgun]','[Drum-Shotgun]','[SMG]','[Rifle]','[AK47]','[AR]','[AUG]','[DrumGun]','[P90]','[LMG]','[Knife]'}
local taBox=CreateSection(Pages.Aim.L,"TargetAim")
CreateToggle(taBox,"TargetAim",function() return Config.Settings['Target Aim'] end,function(v) Config.Settings['Target Aim']=v end)
CreateToggle(taBox,"KnockCheck",function() return Config.Settings['Knock Check'] end,function(v) Config.Settings['Knock Check']=v end)
CreateToggle(taBox,"VisibleCheck",function() return Config.Settings['Visible Check'] end,function(v) Config.Settings['Visible Check']=v end)
local aaBox=CreateSection(Pages.Aim.R,"AimAssist")
local aaBtn=CreateToggle(aaBox,"AimAssist",function() return Config['Aim Assist'].Enabled end,function(v) Config['Aim Assist'].Enabled=v if not v then aimAssistPart=nil aimbotTargetPlayer=nil aimbotTargetPart=nil end end)
attachKeybind(aaBtn,Config.Keybinds['Aim Assist'])
CreateDropdown(aaBox,"AssistStyle",{"Mouse","Camera"},function() return Config['Aim Assist'].Style end,function(v) Config['Aim Assist'].Style=v end)
CreateSlider(aaBox,"HSmoothness",1,20,function() return Config['Aim Assist'].HSmoothness end,function(v) Config['Aim Assist'].HSmoothness=v end)
CreateSlider(aaBox,"VSmoothness",1,20,function() return Config['Aim Assist'].VSmoothness end,function(v) Config['Aim Assist'].VSmoothness=v end)
CreateDropdown(aaBox,"SmoothStyle",{"Direction","Uniform"},function() return Config['Aim Assist'].SmoothStyle end,function(v) Config['Aim Assist'].SmoothStyle=v end)
CreateToggle(aaBox,"AutoPrediction",function() return Config['Aim Assist'].AutoPrediction~=false end,function(v) Config['Aim Assist'].AutoPrediction=v end)
CreateSlider(aaBox,"HPrediction",0,1000,function() return math.floor(Config['Aim Assist'].HPrediction*1000) end,function(v) Config['Aim Assist'].HPrediction=v/1000 end)
CreateSlider(aaBox,"VPrediction",0,1000,function() return math.floor(Config['Aim Assist'].VPrediction*1000) end,function(v) Config['Aim Assist'].VPrediction=v/1000 end)
CreateSlider(aaBox,"JumpOffset",-30,30,function() return math.floor(Config['Aim Assist'].JumpOffset*10) end,function(v) Config['Aim Assist'].JumpOffset=v/10 end)
CreateSlider(aaBox,"Multipoint",0,100,function() return Config['Aim Assist'].Multipoint end,function(v) Config['Aim Assist'].Multipoint=v end)
CreateToggle(aaBox,"DontAimVertically",function() return Config['Aim Assist'].DontAimVertically end,function(v) Config['Aim Assist'].DontAimVertically=v end)
CreateToggle(aaBox,"JumpPrediction",function() return Config['Aim Assist'].JumpPrediction end,function(v) Config['Aim Assist'].JumpPrediction=v end)
CreateSlider(aaBox,"JumpPredictionVal",0,400,function() return math.floor((Config['Aim Assist'].JumpPredictionValue or 0.1)*1000) end,function(v) Config['Aim Assist'].JumpPredictionValue=v/1000 end)
CreateLabel(aaBox,T("AimTargetHelp"))
aaStatus=CreateDynLabel(aaBox,function()
	local AA=Config['Aim Assist']
	if not AA.Enabled then return T("AimStatusOff") end
	if aimbotTargetPlayer then
		return T("AimStatusLocked")..": "..tostring(aimbotTargetPlayer.Name).."  "..T("AimStatusFound")..": "..tostring(aaStatusFound or 0)
	end
	return T("AimStatusNone").."  "..T("AimStatusFound")..": "..tostring(aaStatusFound or 0)
end)
CreateToggle(aaBox,"AutoSelect",function() return Config['Aim Assist'].AutoSelect end,function(v) Config['Aim Assist'].AutoSelect=v end)
CreateSlider(aaBox,"AutoSelectDelay",5,1000,function() return math.floor(Config['Aim Assist'].AutoSelectDelay*1000) end,function(v) Config['Aim Assist'].AutoSelectDelay=v/1000 end)
CreateToggle(aaBox,"AimSticky",function() return Config['Aim Assist'].Sticky end,function(v) Config['Aim Assist'].Sticky=v end)
CreateDropdown(aaBox,"AimHitPart",{"Head","UpperTorso","HumanoidRootPart","LowerTorso","Closest Part"},function() return Config['Aim Assist'].HitPart end,function(v) Config['Aim Assist'].HitPart=v end)
CreateDropdown(aaBox,"AimAirHitPart",{"Head","UpperTorso","HumanoidRootPart","LowerTorso"},function() return Config['Aim Assist'].AirHitPart end,function(v) Config['Aim Assist'].AirHitPart=v end)
CreateSlider(aaBox,"AimMaxDist",0,3000,function() return Config['Aim Assist'].MaxDistance end,function(v) Config['Aim Assist'].MaxDistance=v end)
CreateToggle(aaBox,"AimWallCheck",function() return Config['Aim Assist'].WallCheck end,function(v) Config['Aim Assist'].WallCheck=v end)
CreateToggle(aaBox,"AAUseFOV",function() return Config['Aim Assist'].UseFOV end,function(v) Config['Aim Assist'].UseFOV=v;updateAimFOV() end)
CreateColorPicker(aaBox,"AAFOVColor",function() return Config['Aim Assist'].FOVColor end,function(v) Config['Aim Assist'].FOVColor=v;updateAimFOV() end)
CreateSlider(aaBox,"AAFOVSize",50,1500,function() return Config['Aim Assist'].FOVSize end,function(v) Config['Aim Assist'].FOVSize=v;updateAimFOV() end)
CreateSlider(aaBox,"AAFOVThick",1,10,function() return Config['Aim Assist'].FOVThickness end,function(v) Config['Aim Assist'].FOVThickness=v;updateAimFOV() end)
CreateToggle(aaBox,"AAFOVVisible",function() return Config['Aim Assist'].FOVVisible end,function(v) Config['Aim Assist'].FOVVisible=v;updateAimFOV() end)
CreateToggle(aaBox,"AAFOVMouse",function() return Config['Aim Assist'].FOVMouse==true end,function(v) Config['Aim Assist'].FOVMouse=v;updateAimFOV() end)
CreateToggle(aaBox,"FallbackCamera",function() return Config['Aim Assist'].FallbackCamera end,function(v) Config['Aim Assist'].FallbackCamera=v end)


end
do
local VA=Config['Visual Awareness']
local espBox=CreateSection(Pages.Visuals.L,"ESP")
local espBtn=CreateToggle(espBox,"ESP",function() return VA.Enabled end,function(v) VA.Enabled=v end)
attachKeybind(espBtn,Config.Keybinds['ESP'])
CreateToggle(espBox,"ESPNames",function() return VA.Names end,function(v) VA.Names=v end)
CreateColorPicker(espBox,"NameTagColor",function() return VA.NameTagColor end,function(v) VA.NameTagColor=v end)
CreateSlider(espBox,"NameTagSize",8,24,function() return VA.NameTagSize end,function(v) VA.NameTagSize=v end)
CreateDropdown(espBox,"ESPNameMode",{"Username","DisplayName","Username (DisplayName)","Username (DisplayName) [UserID]"},function() return VA.NameMode end,function(v) VA.NameMode=v end)
CreateToggle(espBox,"ESPOutline",function() return VA.Outline end,function(v) VA.Outline=v end)
CreateToggle(espBox,"ESPBox",function() return VA.Box.Enabled end,function(v) VA.Box.Enabled=v end)
CreateColorPicker(espBox,"BoxColor",function() return VA.Box.Color end,function(v) VA.Box.Color=v end)
CreateSlider(espBox,"BoxThick",1,5,function() return VA.Box.Thickness end,function(v) VA.Box.Thickness=v end)
CreateToggle(espBox,"ESPFill",function() return VA.Fill.Enabled end,function(v) VA.Fill.Enabled=v end)
CreateToggle(espBox,"ESPChams",function() return VA.Chams.Enabled end,function(v) VA.Chams.Enabled=v end)
CreateToggle(espBox,"ESPArmor",function() return VA.ArmorBar.Enabled end,function(v) VA.ArmorBar.Enabled=v end)
CreateToggle(espBox,"WeaponESP",function() return VA.WeaponESP end,function(v) VA.WeaponESP=v end)
CreateColorPicker(espBox,"WeaponESPColor",function() return VA.WeaponESPColor end,function(v) VA.WeaponESPColor=v end)
CreateSlider(espBox,"WeaponESPSize",8,24,function() return VA.WeaponESPSize end,function(v) VA.WeaponESPSize=v end)
CreateToggle(espBox,"DistanceESP",function() return VA.Distance and VA.Distance.Enabled end,function(v) VA.Distance=VA.Distance or {Enabled=false,Size=11,Color=Color3.fromRGB(255,255,255)};VA.Distance.Enabled=v end)
CreateColorPicker(espBox,"DistColor",function() return VA.Distance and VA.Distance.Color or Color3.fromRGB(255,255,255) end,function(v) VA.Distance=VA.Distance or {Enabled=false,Size=11,Color=Color3.fromRGB(255,255,255)};VA.Distance.Color=v end)
CreateSlider(espBox,"DistSize",8,24,function() return VA.Distance and VA.Distance.Size or 11 end,function(v) VA.Distance=VA.Distance or {Enabled=false,Size=11,Color=Color3.fromRGB(255,255,255)};VA.Distance.Size=v end)
CreateToggle(espBox,"Tracer",function() return VA.Line.Enabled end,function(v) VA.Line.Enabled=v end)
CreateColorPicker(espBox,"TracerColor",function() return VA.Line.Color end,function(v) VA.Line.Color=v end)
CreateToggle(espBox,"HealthBar",function() return VA.HealthBar.Enabled end,function(v) VA.HealthBar.Enabled=v end)
CreateToggle(espBox,"HealthText",function() return VA.HealthBar.ShowText end,function(v) VA.HealthBar.ShowText=v end)
CreateToggle(espBox,"Skeleton",function() return VA.Skeleton.Enabled end,function(v) VA.Skeleton.Enabled=v end)
CreateToggle(espBox,"KeybindDisplay",function() return VA.KeybindDisplay end,function(v) VA.KeybindDisplay=v;updateKeybindDisplay() end)
CreateColorPicker(espBox,"KDPColor",function() return VA.KeybindDisplayColor end,function(v) VA.KeybindDisplayColor=v;updateKeybindDisplay() end)
CreateSlider(espBox,"KDPSize",8,40,function() return VA.KeybindDisplaySize end,function(v) VA.KeybindDisplaySize=v;updateKeybindDisplay() end)
CreateDropdown(espBox,"KDPFont",{"Plex","UI","Flex","Monospace"},function() return VA.KeybindDisplayFont end,function(v) VA.KeybindDisplayFont=v;updateKeybindDisplay() end)
CreateToggle(espBox,"AntiRecord",function() return VA.AntiRecord end,function(v) VA.AntiRecord=v end)
local lpBox=CreateSection(Pages.Visuals.L,"LPVisuals")
CreateToggle(lpBox,"Trail",function() return Config['Local Player Visuals'].Trail end,function(v) Config['Local Player Visuals'].Trail=v;applyTrail() end)
CreateColorPicker(lpBox,"TrailColor",function() return Config['Local Player Visuals'].TrailColor end,function(v) Config['Local Player Visuals'].TrailColor=v;applyTrail() end)
CreateToggle(lpBox,"TrailGradient",function() return Config['Local Player Visuals'].TrailGradient end,function(v) Config['Local Player Visuals'].TrailGradient=v;applyTrail() end)
CreateColorPicker(lpBox,"GradientColor",function() return Config['Local Player Visuals'].GradientColor end,function(v) Config['Local Player Visuals'].GradientColor=v;applyTrail() end)
CreateToggle(lpBox,"MaterialTools",function() return Config['Local Player Visuals'].MaterialTools end,function(v) Config['Local Player Visuals'].MaterialTools=v;applyMaterialTools() end)
CreateDropdown(lpBox,"MaterialValue",{"ForceField","Neon","Glass","Ice"},function() return Config['Local Player Visuals'].MaterialToolsValue end,function(v) Config['Local Player Visuals'].MaterialToolsValue=v;applyMaterialTools() end)
CreateColorPicker(lpBox,"MaterialColor",function() return Config['Local Player Visuals'].MaterialToolsColor end,function(v) Config['Local Player Visuals'].MaterialToolsColor=v;applyMaterialTools() end)
CreateToggle(lpBox,"AccessoryAdder",function() return Config['Local Player Visuals'].AccessoryAdder end,function(v)
Config['Local Player Visuals'].AccessoryAdder=v
if not v then removeAllAccessories() end
end)
CreateTextBox(lpBox,"AccessoryID","107473988",function() return accessoryId end,function(v) accessoryId=v end)
CreateButton(lpBox,"AddAccessory",function() addAccessory(accessoryId) end)
CreateButton(lpBox,"RemoveAccessory",function() removeAllAccessories() end)
local dpBox=CreateSection(Pages.Visuals.L,"DesyncPos")
CreateToggle(dpBox,"DesyncPos",function() return Config['Desynced Position'].Enabled end,function(v) Config['Desynced Position'].Enabled=v end)
CreateColorPicker(dpBox,"DesyncPosColor",function() return Config['Desynced Position'].Color end,function(v) Config['Desynced Position'].Color=v end)
CreateColorPicker(dpBox,"DesyncPosOL",function() return Config['Desynced Position'].OutlineColor end,function(v) Config['Desynced Position'].OutlineColor=v end)
CreateDropdown(dpBox,"DesyncPosMat",{"ForceField","Neon"},function() return Config['Desynced Position'].Value end,function(v) Config['Desynced Position'].Value=v end)
CreateToggle(dpBox,"DesyncPosHL",function() return Config['Desynced Position'].Highlight end,function(v) Config['Desynced Position'].Highlight=v end)
CreateColorPopupButton(espBox,"ESPColors",{
{"ESPColor",function() return VA.Color end,function(v) VA.Color=v end},
{"TargetColor",function() return VA.TargetColor end,function(v) VA.TargetColor=v end},
{"WLColor",function() return VA.WhitelistColor end,function(v) VA.WhitelistColor=v end},
})
local efBox=CreateSection(Pages.Visuals.L,"Effects")
CreateToggle(efBox,"LocalTracers",function() return VA.Tracers.Enabled end,function(v) VA.Tracers.Enabled=v end)
CreateColorPicker(efBox,"TracerColor",function() return VA.Tracers.Color end,function(v) VA.Tracers.Color=v end)
CreateDropdown(efBox,"TracerMode",{"Line","Beam","Neon"},function() return VA.Tracers.Value end,function(v) VA.Tracers.Value=v end)
CreateDropdown(efBox,"TracerTexture",{"Laser","Beam"},function() return VA.Tracers.Texture end,function(v) VA.Tracers.Texture=v end)
CreateSlider(efBox,"TracerLife",1,20,function() return math.floor(VA.Tracers.Life*10) end,function(v) VA.Tracers.Life=v/10 end)
CreateToggle(efBox,"EnemyTracers",function() return VA.EnemyTracers.Enabled end,function(v) VA.EnemyTracers.Enabled=v end)
CreateColorPicker(efBox,"EnemyTracerColor",function() return VA.EnemyTracers.Color end,function(v) VA.EnemyTracers.Color=v end)
CreateDropdown(efBox,"EnemyTracerMode",{"Line","Beam","Neon"},function() return VA.EnemyTracers.Value end,function(v) VA.EnemyTracers.Value=v end)
CreateSlider(efBox,"EnemyTracerLife",1,20,function() return math.floor(VA.EnemyTracers.Life*10) end,function(v) VA.EnemyTracers.Life=v/10 end)
CreateToggle(efBox,"Impacts",function() return VA.Impacts.Enabled end,function(v) VA.Impacts.Enabled=v end)
CreateSlider(efBox,"ImpactSize",1,10,function() return math.floor(VA.Impacts.Size*10) end,function(v) VA.Impacts.Size=v/10 end)
local ohBox=CreateSection(Pages.Visuals.L,"OnHit")
CreateToggle(ohBox,"DamageNumber",function() return VA.DamageNumber.Enabled end,function(v) VA.DamageNumber.Enabled=v end)
CreateDropdown(ohBox,"DamageMode",{"Float","Still"},function() return VA.DamageNumber.Value end,function(v) VA.DamageNumber.Value=v end)
CreateSlider(ohBox,"DamageLife",1,25,function() return math.floor(VA.DamageNumber.Life*10) end,function(v) VA.DamageNumber.Life=v/10 end)
CreateToggle(ohBox,"HitMarker",function() return VA.HitMarker.Enabled end,function(v) VA.HitMarker.Enabled=v end)
CreateDropdown(ohBox,"HitMarkerMode",{"2D","3D"},function() return VA.HitMarker.Value end,function(v) VA.HitMarker.Value=v end)
CreateToggle(ohBox,"HitChams",function() return VA.HitChams.Enabled end,function(v) VA.HitChams.Enabled=v end)
CreateDropdown(ohBox,"HitChamsMode",{"Outline","ForceField","Neon"},function() return VA.HitChams.Value end,function(v) VA.HitChams.Value=v end)
CreateToggle(ohBox,"OnlyLast",function() return VA.HitChams.OnlyLast end,function(v) VA.HitChams.OnlyLast=v end)
CreateToggle(ohBox,"FadeOut",function() return VA.HitChams.FadeOut end,function(v) VA.HitChams.FadeOut=v end)
CreateSlider(ohBox,"ChamsLife",1,20,function() return math.floor(VA.HitChams.Life*10) end,function(v) VA.HitChams.Life=v/10 end)
CreateToggle(ohBox,"HitSkeleton",function() return VA.HitSkeleton.Enabled end,function(v) VA.HitSkeleton.Enabled=v end)
CreateToggle(ohBox,"HitSkeletonOnly",function() return VA.HitSkeleton.OnlyLast end,function(v) VA.HitSkeleton.OnlyLast=v end)
CreateToggle(ohBox,"HitParticle",function() return VA.HitParticle.Enabled end,function(v) VA.HitParticle.Enabled=v end)
CreateDropdown(ohBox,"HitParticleValue",{"Sparks","Splash","Flame","Bubble","Bits","Air"},function() return VA.HitParticle.Value end,function(v) VA.HitParticle.Value=v end)
CreateToggle(ohBox,"HitSound",function() return VA.HitSound.Enabled end,function(v) VA.HitSound.Enabled=v end)
CreateDropdown(ohBox,"HitSoundValue",{"Bubble","Lazer","Pick","Pop","Rust","Sans","Fart","Big","Vine","UwU","Bruh","Skeet","Neverlose","Fatality","Bonk","Minecraft","Gamesense","RIFK7","Bamboo","Crowbar","Weeb","Beep","Bambi","Stone","Old Fatality","Click","Ding","Snow","Laser","Mario","Steve","Call of Duty","Bat","TF2 Critical","Saber","Baimware","Osu","TF2","Slime","Among Us","One","Custom"},function() return VA.HitSound.Value end,function(v) VA.HitSound.Value=v end)
CreateSlider(ohBox,"HitSoundVolume",0,100,function() return VA.HitSound.Volume end,function(v) VA.HitSound.Volume=v end)
local wBox=CreateSection(Pages.Visuals.R,"World")
CreateToggle(wBox,"WorldMod",function() return VA.WorldMod.Enabled end,function(v) VA.WorldMod.Enabled=v;applyWorld() end)
CreateSlider(wBox,"Brightness",0,10,function() return VA.WorldMod.Brightness end,function(v) VA.WorldMod.Brightness=v end)
CreateSlider(wBox,"FogEnd",0,10000,function() return VA.WorldMod.FogEnd end,function(v) VA.WorldMod.FogEnd=v end)
CreateSlider(wBox,"TimeChanger",0,24,function() return VA.WorldMod.ClockTime end,function(v) VA.WorldMod.ClockTime=v end)
CreateToggle(wBox,"Skybox",function() return VA.Skybox.Enabled end,function(v) VA.Skybox.Enabled=v;applyWorld() end)
CreateDropdown(wBox,"Skybox",{"Jungle","Blossom","Red night","Purple default","Foggy"},function() return VA.Skybox.Value end,function(v) VA.Skybox.Value=v;applyWorld() end)
CreateToggle(wBox,"AspectRatio",function() return VA.AspectRatio.Enabled end,function(v) VA.AspectRatio.Enabled=v;applyAspect() end)
CreateToggle(wBox,"Atmosphere",function() return VA.WorldMod.Atmosphere end,function(v) VA.WorldMod.Atmosphere=v;applyWorld() end)
CreateColorPicker(wBox,"AtmosphereColor",function() return VA.WorldMod.AtmosphereColor end,function(v) VA.WorldMod.AtmosphereColor=v;applyWorld() end)
CreateColorPicker(wBox,"AtmosphereDecay",function() return VA.WorldMod.AtmosphereDecay end,function(v) VA.WorldMod.AtmosphereDecay=v;applyWorld() end)
CreateSlider(wBox,"AtmosphereDensity",0,100,function() return math.floor(VA.WorldMod.AtmosphereDensity*100) end,function(v) VA.WorldMod.AtmosphereDensity=v/100;applyWorld() end)
CreateSlider(wBox,"AtmosphereGlare",0,100,function() return VA.WorldMod.AtmosphereGlare end,function(v) VA.WorldMod.AtmosphereGlare=v;applyWorld() end)
CreateSlider(wBox,"AtmosphereHaze",0,100,function() return VA.WorldMod.AtmosphereHaze end,function(v) VA.WorldMod.AtmosphereHaze=v;applyWorld() end)
CreateSlider(wBox,"Saturation",-5,5,function() return VA.WorldMod.Saturation end,function(v) VA.WorldMod.Saturation=v;applyWorld() end)
CreateSlider(wBox,"AspectValue",1,100,function() return VA.AspectRatio.Value end,function(v) VA.AspectRatio.Value=v;applyAspect() end)
local vBox=CreateSection(Pages.Visuals.R,"ViewHud")
CreateToggle(vBox,"UnlockZoom",function() return VA.View.UnlockZoom end,function(v) VA.View.UnlockZoom=v;applyView() end)
CreateToggle(vBox,"HideGunCrosshair",function() return VA.View.HideGunCrosshair end,function(v) VA.View.HideGunCrosshair=v;applyView() end)
CreateToggle(vBox,"HideCursor",function() return VA.View.HideCursor end,function(v) VA.View.HideCursor=v;applyView() end)
CreateToggle(vBox,"ShowChat",function() return VA.View.ShowChat end,function(v) VA.View.ShowChat=v;applyView() end)
CreateToggle(vBox,"Crosshair",function() return VA.Crosshair.Enabled end,function(v) VA.Crosshair.Enabled=v end)
CreateSlider(vBox,"CrossSize",2,40,function() return VA.Crosshair.Size end,function(v) VA.Crosshair.Size=v end)
CreateToggle(vBox,"CrossFollow",function() return VA.Crosshair.Follow end,function(v) VA.Crosshair.Follow=v end)
CreateDropdown(vBox,"CrossLoc",{"Mouse","Center"},function() return VA.Crosshair.Location end,function(v) VA.Crosshair.Location=v end)
CreateSlider(vBox,"CrossSmooth",0,100,function() return VA.Crosshair.Smooth end,function(v) VA.Crosshair.Smooth=v end)
CreateSlider(vBox,"CrossSpin",0,100,function() return VA.Crosshair.Spin end,function(v) VA.Crosshair.Spin=v end)
CreateSlider(vBox,"CrossGap",0,20,function() return VA.Crosshair.Gap end,function(v) VA.Crosshair.Gap=v end)
CreateToggle(vBox,"Watermark",function() return VA.Watermark.Enabled end,function(v) VA.Watermark.Enabled=v end)
CreateSlider(vBox,"WaterSize",8,24,function() return VA.Watermark.Size end,function(v) VA.Watermark.Size=v end)
CreateTextBox(vBox,"WaterText","hate.CC",function() return VA.Watermark.Text end,function(v) VA.Watermark.Text=v end)
CreateDropdown(vBox,"WaterPos",{"Center","Mouse"},function() return VA.Watermark.Position end,function(v) VA.Watermark.Position=v end)
CreateSlider(vBox,"WaterY",-400,400,function() return VA.Watermark.YOffset end,function(v) VA.Watermark.YOffset=v end)
CreateToggle(vBox,"Notifications",function() return VA.Notifications.Enabled end,function(v) VA.Notifications.Enabled=v end)
CreateDropdown(vBox,"NotifStyle",{"Simple","Gamesense","Gamesensical"},function() return VA.Notifications.Style end,function(v) VA.Notifications.Style=v end)
CreateToggle(vBox,"MoneyText",function() return VA.MoneyText.Enabled end,function(v) VA.MoneyText.Enabled=v end)
CreateDropdown(vBox,"MoneyStyle",{"Default","Simple"},function() return VA.MoneyText.Value end,function(v) VA.MoneyText.Value=v end)
CreateDropdown(vBox,"MoneyImage",{"None","My Melody","Custom"},function() return VA.MoneyText.Image end,function(v) VA.MoneyText.Image=v end)
CreateToggle(vBox,"StatBars",function() return VA.StatBars.Enabled end,function(v) VA.StatBars.Enabled=v end)
CreateDropdown(vBox,"StatStyle",{"Default","Flat","Minimalistic","Gamesense","Minecraft","Sanrio"},function() return VA.StatBars.Value end,function(v) VA.StatBars.Value=v end)
CreateColorPopupButton(vBox,"StatColors",{
{"HP",function() return VA.StatBars.HP end,function(v) VA.StatBars.HP=v end},
{"Energy",function() return VA.StatBars.Energy end,function(v) VA.StatBars.Energy=v end},
{"Armor",function() return VA.StatBars.Armor end,function(v) VA.StatBars.Armor=v end},
{"Fire",function() return VA.StatBars.Fire end,function(v) VA.StatBars.Fire=v end},
})
CreateToggle(vBox,"Hotbar",function() return VA.Hotbar.Enabled end,function(v) VA.Hotbar.Enabled=v end)
CreateDropdown(vBox,"HotbarStyle",{"Default","Minimalistic"},function() return VA.Hotbar.Value end,function(v) VA.Hotbar.Value=v end)
local cssBox=CreateSection(Pages.Visuals.R,"CustomShootSound")
CreateToggle(cssBox,"CustomShoot",function() return Config['Visual Awareness CustomShoot'].Enabled end,function(v) Config['Visual Awareness CustomShoot'].Enabled=v;local ch=LocalPlayer.Character if ch then for _,t in pairs(ch:GetChildren()) do if t:IsA("Tool") then applyShootSoundTool(t) end end end end)
CreateDropdown(cssBox,"ShootSoundValue",{"SSG-08","SCAR20","G3SG1","USP-S","AWP","RIFK7","Bubble","Minecraft","Cod","Bameware","Neverlose","Gamesense","Rust","Custom"},function() return Config['Visual Awareness CustomShoot'].Value end,function(v) Config['Visual Awareness CustomShoot'].Value=v;local ch=LocalPlayer.Character if ch then for _,t in pairs(ch:GetChildren()) do if t:IsA("Tool") then applyShootSoundTool(t) end end end end)
CreateSlider(cssBox,"ShootVolume",1,50,function() return math.floor(Config['Visual Awareness CustomShoot'].Volume*10) end,function(v) Config['Visual Awareness CustomShoot'].Volume=v/10 end)
local llBox=CreateSection(Pages.Visuals.R,"LockLine")
CreateToggle(llBox,"LockLine",function() return Config['Lock Line'].Enabled end,function(v) Config['Lock Line'].Enabled=v end)
CreateColorPicker(llBox,"LockLineColor",function() return Config['Lock Line'].Color end,function(v) Config['Lock Line'].Color=v end)
CreateSlider(llBox,"LockLineThick",1,10,function() return Config['Lock Line'].Thickness end,function(v) Config['Lock Line'].Thickness=v end)
end
do
local mvBox=CreateSection(Pages.Misc.L,"Movement")
local spBtn=CreateToggle(mvBox,"CFrameSpeed",function() return Config.Movement.CFrameSpeed end,function(v) Config.Movement.CFrameSpeed=v end)
attachKeybind(spBtn,Config.Keybinds['Speed'])
CreateSlider(mvBox,"SpeedValue",1,500,function() return Config.Movement.SpeedValue end,function(v) Config.Movement.SpeedValue=v end)
local flyBtn=CreateToggle(mvBox,"CFrameFly",function() return Config.Movement.CFrameFly end,function(v) Config.Movement.CFrameFly=v end)
attachKeybind(flyBtn,Config.Keybinds['Fly'])
CreateSlider(mvBox,"FlyValue",1,500,function() return Config.Movement.FlyValue end,function(v) Config.Movement.FlyValue=v end)
local ncBtn=CreateToggle(mvBox,"Noclip",function() return Config.Movement.Noclip end,function(v) Config.Movement.Noclip=v end)
attachKeybind(ncBtn,Config.Keybinds['Noclip'])
CreateToggle(mvBox,"PreventFling",function() return Config.Movement.PreventFling end,function(v) Config.Movement.PreventFling=v end)
CreateDropdown(mvBox,"Emote",{"Happier Jump","Bouncy Twirl","V Pose"},function() return Config.Movement.Emote end,function(v) Config.Movement.Emote=v end)
local emBtn=CreateToggle(mvBox,"EmoteBind",function() return Config['Emote Bind'].Enabled end,function(v) Config['Emote Bind'].Enabled=v end)
attachKeybind(emBtn,Config.Keybinds['Emote'])
local sjBtn=CreateToggle(mvBox,"SuperJump",function() return Config['Super Jump'].Enabled end,function(v) Config['Super Jump'].Enabled=v end)
attachKeybind(sjBtn,Config.Keybinds['Super Jump'])
CreateSlider(mvBox,"JumpPower",50,500,function() return Config['Super Jump'].Power end,function(v) Config['Super Jump'].Power=v end)
CreateToggle(mvBox,"NoJumpCooldown",function() return Config['No Jump Cooldown'].Enabled end,function(v) Config['No Jump Cooldown'].Enabled=v end)
local aaBox2=CreateSection(Pages.Misc.L,"AntiAim")
CreateToggle(aaBox2,"AnimationLag",function() return Config['Anti Aim'].AnimationLag end,function(v) Config['Anti Aim'].AnimationLag=v end)
CreateSlider(aaBox2,"AnimationLagVal",1,100,function() return Config['Anti Aim'].AnimationLagValue end,function(v) Config['Anti Aim'].AnimationLagValue=v end)
CreateToggle(aaBox2,"AnimationSpam",function() return Config['Anti Aim'].AnimationSpam end,function(v) Config['Anti Aim'].AnimationSpam=v end)
CreateDropdown(aaBox2,"AnimationSpamVal",{"Floss","Hype"},function() return Config['Anti Aim'].AnimationSpamValue end,function(v) Config['Anti Aim'].AnimationSpamValue=v end)
CreateToggle(aaBox2,"ClientPitch",function() return Config['Anti Aim'].ClientPitch end,function(v) Config['Anti Aim'].ClientPitch=v end)
CreateSlider(aaBox2,"ClientPitchVal",-90,90,function() return Config['Anti Aim'].ClientPitchValue end,function(v) Config['Anti Aim'].ClientPitchValue=v end)
CreateToggle(aaBox2,"FaceBackwards",function() return Config['Anti Aim'].FaceBackwards end,function(v) Config['Anti Aim'].FaceBackwards=v end)
CreateToggle(aaBox2,"Spinbot",function() return Config['Anti Aim'].Spinbot end,function(v) Config['Anti Aim'].Spinbot=v end)
CreateSlider(aaBox2,"SpinSpeed",1,100,function() return Config['Anti Aim'].SpinbotSpeed end,function(v) Config['Anti Aim'].SpinbotSpeed=v end)
CreateToggle(aaBox2,"AntiAimViewer",function() return Config['Anti Aim Viewer'].Enabled end,function(v) Config['Anti Aim Viewer'].Enabled=v end)
local dsBox=CreateSection(Pages.Misc.L,"Desync")
CreateLabel(dsBox,"假同步: 视角固定不动, 只有移动时才生效 (站着不动=原地传送), 眼睛实时显示实际位置")
local dsBtn=CreateToggle(dsBox,"Desync",function() return Config['Desync'].Enabled end,function(v) toggleDesync(v) end)
attachKeybind(dsBtn,Config.Keybinds['Desync'])
CreateToggle(dsBox,"MoveOnly",function() return Config['Desync'].MoveOnly end,function(v) Config['Desync'].MoveOnly=v end)
CreateDropdown(dsBox,"DesyncMode",{"Underground","Void"},function() return Config['Desync'].Mode end,function(v) Config['Desync'].Mode=v end)
CreateSlider(dsBox,"DesyncDepth",0,60,function() return Config['Desync'].Depth or 0 end,function(v) Config['Desync'].Depth=v end)
CreateToggle(dsBox,"VelocityDesync",function() return Config['Desync'].Velocity end,function(v) Config['Desync'].Velocity=v end)
CreateDropdown(dsBox,"VelocityMode",{"Zero","Multiplier","Underground","Random","Max","Sky"},function() return Config['Desync'].VelocityValue end,function(v) Config['Desync'].VelocityValue=v end)
CreateSlider(dsBox,"MultiplierVal",-40,40,function() return math.floor(Config['Desync'].Multiplier*10) end,function(v) Config['Desync'].Multiplier=v/10 end)
CreateSlider(dsBox,"RandomVal",1,100,function() return Config['Desync'].Random end,function(v) Config['Desync'].Random=v end)
CreateToggle(dsBox,"NetworkDesync",function() return Config['Desync'].Network end,function(v) Config['Desync'].Network=v end)
CreateDropdown(dsBox,"NetworkMode",{"Simple","Teleport move","Invisible","Lag step","Random"},function() return Config['Desync'].NetworkValue end,function(v) Config['Desync'].NetworkValue=v end)
CreateToggle(dsBox,"RandomTP",function() return Config['Desync'].RandomTeleport end,function(v) Config['Desync'].RandomTeleport=v end)
CreateSlider(dsBox,"TPHOff",0,1000,function() return Config['Desync'].HOffset end,function(v) Config['Desync'].HOffset=v end)
CreateSlider(dsBox,"TPVOff",0,1000,function() return Config['Desync'].VOffset end,function(v) Config['Desync'].VOffset=v end)
CreateToggle(dsBox,"ShowEye",function() return Config['Desync'].ShowEye end,function(v) Config['Desync'].ShowEye=v end)
CreateSlider(dsBox,"EyeSize",6,60,function() return Config['Desync'].EyeSize end,function(v) Config['Desync'].EyeSize=v end)
CreateColorPicker(dsBox,"EyeColor",function() return Config['Desync'].EyeColor end,function(v) Config['Desync'].EyeColor=v end)
local skBox=CreateSection(Pages.Misc.L,"SkinChanger")
CreateToggle(skBox,"SkinChanger",function() return Config['Skin Changer'].Enabled end,function(v) Config['Skin Changer'].Enabled=v end)
CreateDropdown(skBox,"SkinWeapon",{'[Revolver]','[Deagle]','[Glock]','[Silencer]','[Double-Barrel SG]','[TacticalShotgun]','[Shotgun]','[Drum-Shotgun]','[SMG]','[Rifle]','[AK47]','[AR]','[AUG]','[DrumGun]','[P90]','[LMG]','[Knife]'},function() return selectedSkinWeapon end,function(v) selectedSkinWeapon=v end)
CreateButton(skBox,"SkinSelect",function() openGridPopup(T("SkinSelect"),{{name=T("SkinSelect"),items=GetSkinList(selectedSkinWeapon)}},false,nil,function(s) if s=='None' then Config['Skin Changer'].Skins[selectedSkinWeapon]=nil else Config['Skin Changer'].Skins[selectedSkinWeapon]=s end end) end)
local puBox=CreateSection(Pages.Misc.L,"Purchases")
CreateButton(puBox,"BuyItem",function() openGridPopup(T("BuyItem"),shopCategories(true),false,nil,function(item) purchaseItem(item) end) end)
CreateLabel(puBox,"购买: 左键单击购买, 名字跟随设置语言翻译")
CreateToggle(puBox,"AutoArmor",function() return Config.Purchases.AutoArmor end,function(v) Config.Purchases.AutoArmor=v end)
CreateSlider(puBox,"ArmorAt",1,100,function() return Config.Purchases.ArmorAt end,function(v) Config.Purchases.ArmorAt=v end)
local amBox=CreateSection(Pages.Misc.L,"AutoAmmo")
CreateToggle(amBox,"AutoAmmo",function() return Config['Auto Ammo'].Enabled end,function(v) Config['Auto Ammo'].Enabled=v end)
CreateSlider(amBox,"AutoAmmoAmount",1,1000,function() return Config['Auto Ammo'].Amount end,function(v) Config['Auto Ammo'].Amount=v end)
local abBox=CreateSection(Pages.Misc.L,"AutoBuy")
local abBtn=CreateToggle(abBox,"AutoBuy",function() return Config['Auto Buy'].Enabled end,function(v) Config['Auto Buy'].Enabled=v end)
attachKeybind(abBtn,Config.Keybinds['Auto Buy'])
CreateLabel(abBox,"自动购买: 按键后依次购买已勾选物品(右键取消勾选)")
CreateButton(abBox,"AutoBuyItems",function()
local curSet={}
for _,it in ipairs(Config['Auto Buy'].Items or {}) do curSet[it]=true end
openGridPopup(T("AutoBuyItems"),shopCategories(true),true,curSet,nil,function(sel)
local list={}
for k,v in pairs(sel) do if v then table.insert(list,k) end end
Config['Auto Buy'].Items=list
Config['Auto Buy'].ItemsSet=sel
end)
end)
-- // [新] RAGEBOT 模块 UI (juju.lol) //
local rbBox=CreateSection(Pages.Misc.R,"Ragebot")
local rbBtn=CreateToggle(rbBox,"Ragebot",function() return Config.Ragebot.Enabled end,function(v)
Config.Ragebot.Enabled=v
if not v then pcall(function() local h=LocalPlayer.Character and LocalPlayer.Character:FindFirstChildOfClass('Humanoid') if h then Camera.CameraSubject=h end end) end
end)
attachKeybind(rbBtn,Config.Keybinds['Ragebot'])
CreateButton(rbBox,"SelectTargets",function()
local names={}
for _,p in ipairs(Players:GetPlayers()) do if p~=LocalPlayer and p.Character then table.insert(names,p.Name) end end
local curSel={}
for _,uid in ipairs(Config.Ragebot.Targets) do local p=Players:GetPlayerByUserId(uid) if p then curSel[p.Name]=true end end
openGridPopup(T("SelectTargets"),{{name=T("SelectTargets"),items=names}},true,curSel,nil,function(s)
local list={}
for n,v in pairs(s or {}) do if v then local p=Players:FindFirstChild(n) if p then table.insert(list,p.UserId) end end end
setRagebotTargets(list)
end)
end)
CreateToggle(rbBox,"IncludeAimbot",function() return Config.Ragebot.IncludeAimbotTarget end,function(v) Config.Ragebot.IncludeAimbotTarget=v end)
CreateToggle(rbBox,"AutoEquip",function() return Config.Ragebot.AutoEquip end,function(v) Config.Ragebot.AutoEquip=v end)
CreateButton(rbBox,"AutoEquipWeapon",function()
local cur={}
for _,w in ipairs(Config.Ragebot.AutoEquipWeapons or {}) do cur[w]=true end
openGridPopup(T("AutoEquipWeapon"),{{name=T("AutoEquipWeapon"),items=WEAPONS}},true,cur,nil,function(sel)
local list={} for k,v in pairs(sel) do if v then table.insert(list,k) end end
Config.Ragebot.AutoEquipWeapons=list
end)
end)
CreateToggle(rbBox,"AttachTarget",function() return Config.Ragebot.AttachToTarget end,function(v) Config.Ragebot.AttachToTarget=v end)
CreateDropdown(rbBox,"AttachMode",{"Strafe","Random Teleport"},function() return Config.Ragebot.AttachMode end,function(v) Config.Ragebot.AttachMode=v end)
CreateSlider(rbBox,"StrafeSpeed",1,100,function() return Config.Ragebot.StrafeSpeed end,function(v) Config.Ragebot.StrafeSpeed=v end)
CreateSlider(rbBox,"HOffset",1,50,function() return Config.Ragebot.HOffset end,function(v) Config.Ragebot.HOffset=v end)
CreateSlider(rbBox,"VOffset",1,50,function() return Config.Ragebot.VOffset end,function(v) Config.Ragebot.VOffset=v end)
CreateToggle(rbBox,"RageDesyncPos",function() return Config.Ragebot.DesyncPosition end,function(v)
Config.Ragebot.DesyncPosition=v
if not v then rageDesyncClear() end
end)
CreateToggle(rbBox,"TeleportBullets",function() return Config.Ragebot.TeleportBullets end,function(v) Config.Ragebot.TeleportBullets=v end)
CreateToggle(rbBox,"ViewTarget",function() return Config.Ragebot.ViewTarget end,function(v)
Config.Ragebot.ViewTarget=v
if not v then pcall(function() local h=LocalPlayer.Character and LocalPlayer.Character:FindFirstChildOfClass('Humanoid') if h then Camera.CameraSubject=h end end) end
end)
CreateToggle(rbBox,"AutoShoot",function() return Config.Ragebot.AutoShoot end,function(v) Config.Ragebot.AutoShoot=v end)
CreateToggle(rbBox,"AutoStomp",function() return Config.Ragebot.AutoStomp end,function(v) Config.Ragebot.AutoStomp=v end)
CreateToggle(rbBox,"TeleportBack",function() return Config.Ragebot.TeleportBack end,function(v) Config.Ragebot.TeleportBack=v end)
CreateToggle(rbBox,"Resolver",function() return Config['Resolver'].Enabled end,function(v) Config['Resolver'].Enabled=v end)
CreateToggle(rbBox,"ResolverRT",function() return Config['Resolver'].RandomTeleport end,function(v) Config['Resolver'].RandomTeleport=v end)
CreateToggle(rbBox,"ResolverNet",function() return Config['Resolver'].Network end,function(v) Config['Resolver'].Network=v end)
CreateSlider(rbBox,"RefreshRate",10,500,function() return math.floor(Config['Resolver'].RefreshRate*1000) end,function(v) Config['Resolver'].RefreshRate=v/1000 end)
CreateToggle(rbBox,"WallCheck",function() return Config.Ragebot.WallCheck end,function(v) Config.Ragebot.WallCheck=v end)
CreateToggle(rbBox,"RageInfRange",function() return Config.Ragebot.InfiniteRange end,function(v) Config.Ragebot.InfiniteRange=v end)
CreateToggle(rbBox,"RageDisableKnocked",function() return Config.Ragebot.DisableIfKnocked end,function(v) Config.Ragebot.DisableIfKnocked=v end)
CreateSlider(rbBox,"RageMaxDist",50,2000,function() return Config.Ragebot.MaxDistance or 500 end,function(v) Config.Ragebot.MaxDistance=v end)
local dcBox=CreateSection(Pages.Misc.R,"DelayChanger")
CreateToggle(dcBox,"DelayChanger",function() return Config['Delay Changer'].Enabled end,function(v) Config['Delay Changer'].Enabled=v end)
CreateSlider(dcBox,"DelayMs",0,1000,function() return math.floor(Config['Delay Changer'].Delay*1000) end,function(v) Config['Delay Changer'].Delay=v/1000 end)
local nsBox=CreateSection(Pages.Misc.R,"NoSpread")
CreateToggle(nsBox,"NoSpread",function() return Config.Spread.Enabled end,function(v) Config.Spread.Enabled=v end)
CreateSlider(nsBox,"SpreadAmount",0,100,function() return Config.Spread.Amount end,function(v) Config.Spread.Amount=v end)
local rfBox=CreateSection(Pages.Misc.R,"RapidFire")
CreateToggle(rfBox,"RapidFire",function() return Config['Rapid Fire'].Enabled end,function(v) Config['Rapid Fire'].Enabled=v end)
CreateSlider(rfBox,"RapidDelay",10,1000,function() return math.floor(Config['Rapid Fire'].Delay*1000) end,function(v) Config['Rapid Fire'].Delay=v/1000 end)
CreateToggle(rfBox,"RapidFireV2",function() return Config['Rapid Fire v2'].Enabled end,function(v) Config['Rapid Fire v2'].Enabled=v;if v then for _,o in ipairs(game:GetDescendants()) do if o.Name=='ToleranceCooldown' and o:IsA('ValueBase') then o.Value=0 end end end end)
CreateToggle(rfBox,"RemoveShootAnim",function() return Config['Remove Shoot Animations'].Enabled end,function(v) Config['Remove Shoot Animations'].Enabled=v end)
local irBox=CreateSection(Pages.Misc.R,"InfRange")
local irBtn=CreateToggle(irBox,"InfRange",function() return Config['Infinite Range'].Enabled end,function(v) Config['Infinite Range'].Enabled=v end)
attachKeybind(irBtn,Config.Keybinds['Inf Range'])
CreateSlider(irBox,"InfMaxRange",100,999999,function() return Config['Infinite Range'].MaxRange end,function(v) Config['Infinite Range'].MaxRange=v end)
local hbBox=CreateSection(Pages.Misc.R,"HitboxExp")
CreateToggle(hbBox,"HitboxExp",function() return Config['Hitbox Expander'].Enabled end,function(v) Config['Hitbox Expander'].Enabled=v end)
CreateSlider(hbBox,"HitboxSize",1,20,function() return Config['Hitbox Expander'].Size end,function(v) Config['Hitbox Expander'].Size=v end)
local utBox=CreateSection(Pages.Misc.R,"Utility")
CreateToggle(utBox,"AntiTrip",function() return Config.Utility.AntiTrip end,function(v) Config.Utility.AntiTrip=v end)
CreateToggle(utBox,"AntiStomp",function() return Config.Utility.AntiStomp end,function(v) Config.Utility.AntiStomp=v end)
CreateToggle(utBox,"CleanScripts",function() return Config.Utility.CleanScripts end,function(v) Config.Utility.CleanScripts=v end)
CreateToggle(utBox,"NoRecoil",function() return Config.Utility.NoRecoil end,function(v) Config.Utility.NoRecoil=v end)
CreateToggle(utBox,"AutoReload",function() return Config.Utility.AutoReload end,function(v) Config.Utility.AutoReload=v end)
CreateToggle(utBox,"SmartAutoReload",function() return Config.Utility.SmartAutoReload end,function(v) Config.Utility.SmartAutoReload=v end)
CreateToggle(utBox,"Pqnd4Kick",function() return Config['Pqnd4 Kick'].Enabled end,function(v) Config['Pqnd4 Kick'].Enabled=v;if v then pqndCreateTool() else pqndRemoveTool() end end)
CreateSlider(utBox,"SmartReloadDelay",0,100,function() return math.floor(Config.Utility.SmartAutoReloadDelay*100) end,function(v) Config.Utility.SmartAutoReloadDelay=v/100 end)
CreateToggle(utBox,"RemoveSlowdowns",function() return Config.Utility.RemoveSlowdowns end,function(v) Config.Utility.RemoveSlowdowns=v;applyRemoveSlowdowns() end)
CreateToggle(utBox,"InstantStand",function() return Config.Utility.InstantStand end,function(v) Config.Utility.InstantStand=v;applyInstantStand() end)
CreateToggle(utBox,"NoSit",function() return Config.Utility.NoSit end,function(v) Config.Utility.NoSit=v;applyNoSit() end)
CreateToggle(utBox,"NoVoidKill",function() return Config.Utility.NoVoidKill end,function(v) Config.Utility.NoVoidKill=v;applyNoVoidKill() end)
CreateToggle(utBox,"AutoSort",function() return Config.Utility.AutoSort end,function(v) Config.Utility.AutoSort=v;if v then doAutoSort() end end)
-- // [juju] AutoSort 9槽方案: 保存当前9格排序为方案, 死亡/乱序后点一次“现在自动排序”即按方案重排 //
local sortPlanName=''
local sortPlanSel=''
local function sortPlanNames()
local names={}
for n in pairs(Config.Utility.SortPlans or {}) do
if type(n)=="string" and n~='' then table.insert(names,n) end
end
table.sort(names)
return names
end
local function sortPlanSelected()
local ns=sortPlanNames()
if ns[1] and (sortPlanSel=='' or not table.find(ns,sortPlanSel)) then sortPlanSel=ns[1] end
return sortPlanSel
end
CreateTextBox(utBox,"SortPlanName","输入方案名称",function() return sortPlanName end,function(v) sortPlanName=v end)
CreateButton(utBox,"SortPlanSave",function()
local name=(sortPlanName or ''):gsub('^%s+',''):gsub('%s+$','')
if name=='' then return end
local bp=LocalPlayer.Backpack
if not bp then return end
local slots={}
local kids=bp:GetChildren()
for i=1,9 do
local c=kids[i]
if c and c:IsA('Tool') then slots[i]=c.Name else slots[i]='' end
end
Config.Utility.SortPlans=Config.Utility.SortPlans or {}
Config.Utility.SortPlans[name]=slots
sortPlanSel=name
end)
local pickBtn=CreateButton(utBox,"SortPlanPick",function()
local ns=sortPlanNames()
if #ns==0 then return end
openDropdown(pickBtn,ns,function(opt) sortPlanSel=opt end)
end)
CreateButton(utBox,"SortPlanApply",function()
local name=sortPlanSelected()
if not name then return end
local plan=Config.Utility.SortPlans and Config.Utility.SortPlans[name]
if not plan then return end
local sl={}
for i=1,9 do sl[i]=plan[i] or '' end
Config.Utility.AutoSortSlots=sl
doAutoSort()
end)
CreateButton(utBox,"SortPlanDel",function()
local name=sortPlanSelected()
if not name or not Config.Utility.SortPlans then return end
Config.Utility.SortPlans[name]=nil
sortPlanSel=''
end)
CreateDynLabel(utBox,function()
local name=sortPlanSelected()
if not name then return T("SortPlanNone") end
local plan=Config.Utility.SortPlans and Config.Utility.SortPlans[name] or {}
local parts={}
for i=1,9 do
if plan[i] and plan[i]~='' then table.insert(parts,i.." "..plan[i]) end
end
return name.."  "..table.concat(parts," | ")
end)
CreateButton(utBox,"AutoSortNow",function() doAutoSort() end)
local dtBox=CreateSection(Pages.Misc.R,"DoubleTap")
CreateToggle(dtBox,"DoubleTap",function() return Config['Double Tap'].Enabled end,function(v) Config['Double Tap'].Enabled=v end)
local spoofBox=CreateSection(Pages.Misc.R,"Spoofing")
CreateToggle(spoofBox,"Headless",function() return Config.Spoofing.Headless end,function(v) Config.Spoofing.Headless=v;if LocalPlayer.Character then ApplyHeadless(LocalPlayer.Character) end end)
CreateToggle(spoofBox,"Korblox",function() return Config.Spoofing.Korblox end,function(v) Config.Spoofing.Korblox=v;if LocalPlayer.Character then ApplyKorblox(LocalPlayer.Character) end end)
end
do
local plBox=CreateSection(Pages.Players.L,"PlayersSection")
local plc=Instance.new("ScrollingFrame");plc.Size=UDim2.new(1,0,0,240);plc.BackgroundTransparency=1;plc.BorderSizePixel=0;plc.ScrollBarThickness=2;plc.ScrollBarImageColor3=UI.Accent;plc.AutomaticCanvasSize=Enum.AutomaticSize.Y;plc.Parent=plBox
local pll=Instance.new("UIListLayout");pll.Padding=UDim.new(0,4);pll.Parent=plc
buildPlayerList=function()
for _,ch in pairs(plc:GetChildren()) do if ch:IsA("Frame") then ch:Destroy() end end
for _,player in pairs(Players:GetPlayers()) do
if player~=LocalPlayer then
local row=Instance.new("Frame");row.Size=UDim2.new(1,0,0,26);row.BackgroundColor3=UI.Panel2;row.BorderSizePixel=0;row.Parent=plc
addStroke(row)
local nl=Instance.new("TextLabel");nl.Size=UDim2.new(1,-190,1,0);nl.Position=UDim2.new(0,8,0,0);nl.BackgroundTransparency=1;nl.Text=player.DisplayName.." @"..player.Name;nl.TextColor3=UI.Text;nl.Font=Enum.Font.Code;nl.TextSize=11;nl.TextXAlignment=Enum.TextXAlignment.Left;nl.TextTruncate=Enum.TextTruncate.AtEnd;nl.Parent=row
local tpBtn=Instance.new("TextButton");tpBtn.Size=UDim2.new(0,30,0,16);tpBtn.AnchorPoint=Vector2.new(1,0.5);tpBtn.Position=UDim2.new(1,-152,0.5,0);tpBtn.Text="TP";tpBtn.Font=Enum.Font.Code;tpBtn.TextSize=10;tpBtn.BorderSizePixel=0;tpBtn.BackgroundColor3=UI.ToggleOff;tpBtn.TextColor3=UI.Text;tpBtn.Parent=row
local tgBtn=Instance.new("TextButton");tgBtn.Size=UDim2.new(0,30,0,16);tgBtn.AnchorPoint=Vector2.new(1,0.5);tgBtn.Position=UDim2.new(1,-118,0.5,0);tgBtn.Text="TG";tgBtn.Font=Enum.Font.Code;tgBtn.TextSize=10;tgBtn.BorderSizePixel=0;tgBtn.TextColor3=UI.Text;tgBtn.Parent=row
local vaBtn=Instance.new("TextButton");vaBtn.Size=UDim2.new(0,30,0,16);vaBtn.AnchorPoint=Vector2.new(1,0.5);vaBtn.Position=UDim2.new(1,-84,0.5,0);vaBtn.Text="VA";vaBtn.Font=Enum.Font.Code;vaBtn.TextSize=10;vaBtn.BorderSizePixel=0;vaBtn.TextColor3=UI.Text;vaBtn.Parent=row
local wlBtn=Instance.new("TextButton");wlBtn.Size=UDim2.new(0,30,0,16);wlBtn.AnchorPoint=Vector2.new(1,0.5);wlBtn.Position=UDim2.new(1,-50,0.5,0);wlBtn.Text="WL";wlBtn.Font=Enum.Font.Code;wlBtn.TextSize=10;wlBtn.BorderSizePixel=0;wlBtn.TextColor3=UI.Text;wlBtn.Parent=row
local rgBtn2=Instance.new("TextButton");rgBtn2.Size=UDim2.new(0,30,0,16);rgBtn2.AnchorPoint=Vector2.new(1,0.5);rgBtn2.Position=UDim2.new(1,-16,0.5,0);rgBtn2.Text="RG";rgBtn2.Font=Enum.Font.Code;rgBtn2.TextSize=10;rgBtn2.BorderSizePixel=0;rgBtn2.TextColor3=UI.Text;rgBtn2.Parent=row
local function updateBtns()
local wl=Whitelist[player.UserId]==true
local tg=Config.Teleport.Target==player.UserId and Config.Teleport.Enabled
local rg=false
local rb=table.find(Config.Ragebot.Targets,player.UserId)~=nil
local va=ViewAimLines[player.UserId]==true
wlBtn.BackgroundColor3=wl and UI.Green or UI.ToggleOff
rgBtn2.BackgroundColor3=rb and Color3.fromRGB(255,0,0) or UI.ToggleOff
tgBtn.BackgroundColor3=tg and UI.Accent or UI.ToggleOff
vaBtn.BackgroundColor3=va and Color3.fromRGB(255,0,255) or UI.ToggleOff
wlBtn.TextColor3=wl and Color3.new(1,1,1) or UI.Text
rgBtn2.TextColor3=(rg or rb) and Color3.new(1,1,1) or UI.Text
tgBtn.TextColor3=tg and Color3.new(1,1,1) or UI.Text
vaBtn.TextColor3=va and Color3.new(1,1,1) or UI.Text
end
tpBtn.MouseButton1Click:Connect(function() teleportToFace(player) end)
tgBtn.MouseButton1Click:Connect(function()
if Config.Teleport.Target==player.UserId and Config.Teleport.Enabled then
Config.Teleport.Enabled=false;Config.Teleport.Target=nil
else Config.Teleport.Target=player.UserId;Config.Teleport.Enabled=true end
buildPlayerList()
end)
vaBtn.MouseButton1Click:Connect(function() if ViewAimLines[player.UserId] then ViewAimLines[player.UserId]=nil else ViewAimLines[player.UserId]=true end updateBtns() end)
wlBtn.MouseButton1Click:Connect(function() if Whitelist[player.UserId] then Whitelist[player.UserId]=nil else Whitelist[player.UserId]=true end updateBtns() end)
rgBtn2.MouseButton1Click:Connect(function()
local nt={}
local has=table.find(Config.Ragebot.Targets,player.UserId)~=nil
for _,uid in ipairs(Config.Ragebot.Targets) do if uid~=player.UserId then table.insert(nt,uid) end end
if not has then table.insert(nt,player.UserId) end
-- // [修复] 走统一入口: 取消 RG 时观战/吸附/子弹传送/解析 等子功能一起对该玩家停止 //
setRagebotTargets(nt)
end)
updateBtns()
end
end
end
buildPlayerList()
track(Players.PlayerAdded:Connect(function() task.wait(1) if not Unloaded then buildPlayerList() end end))
track(Players.PlayerRemoving:Connect(function() task.wait(0.5) if not Unloaded then buildPlayerList() end end))
local tpBox=CreateSection(Pages.Players.R,"Teleport")
CreateToggle(tpBox,"TeleportEnable",function() return Config.Teleport.Enabled end,function(v) Config.Teleport.Enabled=v;buildPlayerList() end)
CreateDropdown(tpBox,"TeleportMode",{"Follow","Orbit"},function() return Config.Teleport.Mode end,function(v) Config.Teleport.Mode=v end)
CreateSlider(tpBox,"TeleportDist",0,50,function() return Config.Teleport.Distance end,function(v) Config.Teleport.Distance=v end)
CreateSlider(tpBox,"TeleportSpeed",0,50,function() return Config.Teleport.Speed end,function(v) Config.Teleport.Speed=v end)
local cfBox=CreateSection(Pages.Players.R,"ConfigSection")
configNameBox=Instance.new("TextBox");configNameBox.Size=UDim2.new(1,-70,0,24);configNameBox.BackgroundColor3=UI.Panel2;configNameBox.BorderSizePixel=0;configNameBox.PlaceholderText=T("ConfigName");configNameBox.Text="";configNameBox.TextColor3=UI.Text;configNameBox.PlaceholderColor3=UI.TextDim;configNameBox.Font=Enum.Font.Code;configNameBox.TextSize=11;configNameBox.ClearTextOnFocus=false;configNameBox.Parent=cfBox
addStroke(configNameBox)
local saveBtn=Instance.new("TextButton");saveBtn.Size=UDim2.new(0,64,0,24);saveBtn.AnchorPoint=Vector2.new(1,0);saveBtn.Position=UDim2.new(1,0,0,0);saveBtn.BackgroundColor3=UI.Accent;saveBtn.BorderSizePixel=0;saveBtn.Font=Enum.Font.Code;saveBtn.TextSize=11;saveBtn.TextColor3=Color3.new(1,1,1);saveBtn.Parent=cfBox
registerLang(saveBtn,"Save");table.insert(AccentElements,saveBtn)
local clc=Instance.new("ScrollingFrame");clc.Size=UDim2.new(1,0,0,140);clc.BackgroundTransparency=1;clc.BorderSizePixel=0;clc.ScrollBarThickness=2;clc.ScrollBarImageColor3=UI.Accent;clc.AutomaticCanvasSize=Enum.AutomaticSize.Y;clc.Parent=cfBox
local cll=Instance.new("UIListLayout");cll.Padding=UDim.new(0,4);cll.Parent=clc
buildConfigList=function()
for _,ch in pairs(clc:GetChildren()) do if ch:IsA("Frame") or ch:IsA("TextLabel") then ch:Destroy() end end
if not filesAvailable() then
local wl=Instance.new("TextLabel");wl.Size=UDim2.new(1,0,0,24);wl.BackgroundTransparency=1;wl.Text=T("NoFiles");wl.TextColor3=UI.Danger;wl.Font=Enum.Font.Code;wl.TextSize=11;wl.Parent=clc
return
end
for _,name in ipairs(listConfigFiles()) do
local row=Instance.new("Frame");row.Size=UDim2.new(1,0,0,24);row.BackgroundColor3=UI.Panel2;row.BorderSizePixel=0;row.Parent=clc
addStroke(row)
local nl=Instance.new("TextLabel");nl.Size=UDim2.new(1,-100,1,0);nl.Position=UDim2.new(0,8,0,0);nl.BackgroundTransparency=1;nl.Text=name;nl.TextColor3=UI.Text;nl.Font=Enum.Font.Code;nl.TextSize=11;nl.TextXAlignment=Enum.TextXAlignment.Left;nl.TextTruncate=Enum.TextTruncate.AtEnd;nl.Parent=row
local loadBtn=Instance.new("TextButton");loadBtn.Size=UDim2.new(0,48,0,16);loadBtn.AnchorPoint=Vector2.new(1,0.5);loadBtn.Position=UDim2.new(1,-44,0.5,0);loadBtn.Text=T("Load");loadBtn.Font=Enum.Font.Code;loadBtn.TextSize=10;loadBtn.BorderSizePixel=0;loadBtn.BackgroundColor3=UI.BG;loadBtn.TextColor3=UI.Accent;loadBtn.Parent=row
addStroke(loadBtn,UI.Accent)
local delBtn=Instance.new("TextButton");delBtn.Size=UDim2.new(0,40,0,16);delBtn.AnchorPoint=Vector2.new(1,0.5);delBtn.Position=UDim2.new(1,-2,0.5,0);delBtn.Text=T("Delete");delBtn.Font=Enum.Font.Code;delBtn.TextSize=10;delBtn.BorderSizePixel=0;delBtn.BackgroundColor3=UI.BG;delBtn.TextColor3=UI.Danger;delBtn.Parent=row
addStroke(delBtn)
loadBtn.MouseButton1Click:Connect(function() if loadConfigFile(name) then refreshAllComponents();buildPlayerList();updateKeybindDisplay() end end)
delBtn.MouseButton1Click:Connect(function() deleteConfigFile(name);buildConfigList() end)
end
end
buildConfigList()
saveBtn.MouseButton1Click:Connect(function()
local name=configNameBox.Text:match("^%s*(.-)%s*$")
if name~="" then saveConfigFile(name);buildConfigList();configNameBox.Text="" end
end)
end
do
local uiBox=CreateSection(Pages.Settings.L,"UIToggleKey")
CreateKeybindRow(uiBox,"UIToggleKey",Config.Keybinds['UI Toggle'])
local uiSetBox=CreateSection(Pages.Settings.L,"UISettings")
CreateSlider(uiSetBox,"UITransparency",0,80,function() return Config['UI Settings'].Transparency end,function(v) Config['UI Settings'].Transparency=v;applyUITransparency() end)
CreateDropdown(uiSetBox,"UIFont",{"Code","Gotham","GothamMedium","RobotoMono","Ubuntu","SourceSans"},function() return Config['UI Settings'].Font end,function(v) Config['UI Settings'].Font=v;UI_Font=fontEnum(v);applyFontAll() end)
CreateToggle(uiSetBox,"RainbowTheme",function() return Config['UI Settings'].Rainbow end,function(v) Config['UI Settings'].Rainbow=v;updateRainbow() end)
CreateToggle(uiSetBox,"HideUserId",function() return Config['UI Settings'].HideUserId end,function(v) Config['UI Settings'].HideUserId=v;applyHideUserId() end)
local thBox=CreateSection(Pages.Settings.L,"ThemeColor")
CreateColorPicker(thBox,"ThemeColor",function() return UI.Accent end,function(v) setAccentColor(v) end)
local lgBox=CreateSection(Pages.Settings.L,"Language")
local LangBtn=Instance.new("TextButton");LangBtn.Size=UDim2.new(1,0,0,24);LangBtn.BackgroundColor3=UI.Panel2;LangBtn.BorderSizePixel=0;LangBtn.Text="";LangBtn.AutoButtonColor=false;LangBtn.Parent=lgBox;addStroke(LangBtn)
local LangLbl=Instance.new("TextLabel");LangLbl.Size=UDim2.new(1,-100,1,0);LangLbl.Position=UDim2.new(0,8,0,0);LangLbl.BackgroundTransparency=1;LangLbl.TextColor3=UI.Text;LangLbl.Font=Enum.Font.Code;LangLbl.TextSize=12;LangLbl.TextXAlignment=Enum.TextXAlignment.Left;LangLbl.Parent=LangBtn;registerLang(LangLbl,"Language")
local LangVal=Instance.new("TextLabel");LangVal.Size=UDim2.new(0,90,1,0);LangVal.Position=UDim2.new(1,-94,0,0);LangVal.BackgroundTransparency=1;LangVal.Text=(CurrentLang=="EN") and "English" or "中文";LangVal.TextColor3=UI.Accent;LangVal.Font=Enum.Font.Code;LangVal.TextSize=11;LangVal.TextXAlignment=Enum.TextXAlignment.Right;LangVal.Parent=LangBtn
table.insert(AccentElements,LangVal)
LangBtn.MouseButton1Click:Connect(function()
CurrentLang=(CurrentLang=="EN") and "CN" or "EN"
LangVal.Text=(CurrentLang=="EN") and "English" or "中文"
refreshLanguage();configNameBox.PlaceholderText=T("ConfigName");buildConfigList();buildPlayerList();updateKeybindDisplay()
end)
local unBox=CreateSection(Pages.Settings.R,"Unload")
local panicLbl=Instance.new("TextLabel");panicLbl.Size=UDim2.new(1,0,0,16);panicLbl.BackgroundTransparency=1;panicLbl.TextColor3=UI.TextDim;panicLbl.Font=Enum.Font.Code;panicLbl.TextSize=10;panicLbl.TextXAlignment=Enum.TextXAlignment.Left;panicLbl.Parent=unBox;registerLang(panicLbl,"PanicInfo")
local UnloadBtn=Instance.new("TextButton");UnloadBtn.Size=UDim2.new(1,0,0,30);UnloadBtn.BackgroundColor3=UI.Panel2;UnloadBtn.BorderSizePixel=0;UnloadBtn.Font=UI_Font;UnloadBtn.TextSize=12;UnloadBtn.TextColor3=UI.Danger;UnloadBtn.AutoButtonColor=false;UnloadBtn.Parent=unBox;registerLang(UnloadBtn,"Unload")
addStroke(UnloadBtn,UI.Danger)
UnloadBtn.MouseEnter:Connect(function() tweenUI(UnloadBtn,{BackgroundColor3=UI.Hover}) end)
UnloadBtn.MouseLeave:Connect(function() tweenUI(UnloadBtn,{BackgroundColor3=UI.Panel2}) end)
UnloadBtn.MouseButton1Click:Connect(UnloadScript)
end
UI_Font=fontEnum(Config['UI Settings'].Font)
applyHideUserId()
applyFontAll()
applyUITransparency()
updateRainbow()
applyAspect()
-- // ============================================================ //
-- // [整合模块] juju Aimbot / 合并假同步 / Feature Indicators    //
-- // ============================================================ //

-- ######################## 瞄准辅助 Aim Assist (juju Legit 页移植, 已合并原 Aimbot) ########################
aimbotTargetPlayer=nil
aimbotTargetPart=nil
aimAssistPart=nil
aimAssistLocked=false
targetBindLocked=false
aaFovCircle=Drawing.new("Circle");aaFovCircle.Visible=false;aaFovCircle.NumSides=72;aaFovCircle.Filled=false
local aimbotLastSelect=0
local aimCamActive=false

local pingSamples={};local pingBase=0;local lastPingSample=0
local function serverPing()
	local val=0
	pcall(function()
		local s=game:GetService("Stats").Network.ServerStatsItem["Data Ping"]
		val=tonumber(string.split(s:GetValueString(),'(')[1]) or 0
	end)
	if tick()-lastPingSample>1 then
		lastPingSample=tick()
		if #pingSamples>=10 then table.remove(pingSamples,1) end
		pingSamples[#pingSamples+1]=val
		local tot=0 for _,v in ipairs(pingSamples) do tot=tot+v end
		if #pingSamples>0 then pingBase=tot/#pingSamples end
	end
	return val
end

local function partVelocity(p)
	local v=p.AssemblyLinearVelocity
	if typeof(v)~="Vector3" then v=p.Velocity or Vector3.new() end
	return v
end


-- // [重写] 命中部位/最大距离/隔墙 等目标条件全部归到"瞄准辅助"名下 (原 Aimbot 模块已删除) //
local function aimHitPart(AA,ch)
	local inAir=false
	local hum=ch:FindFirstChildOfClass('Humanoid')
	local root=ch:FindFirstChild('HumanoidRootPart')
	if hum and root then pcall(function() inAir=(hum.FloorMaterial==Enum.Material.Air and math.abs(root.Velocity.Y)>0) end) end
	local want=(inAir and (AA.AirHitPart or 'LowerTorso')) or (AA.HitPart or 'Head')
	if want=='Closest Part' then return getClosestBodyPart(ch) end
	-- // [修复] 部位缺失时逐级兜底, 不会因为某个部件不存在就整个选不到目标 //
	return ch:FindFirstChild(want) or ch:FindFirstChild('UpperTorso') or ch:FindFirstChild('HumanoidRootPart') or ch:FindFirstChild('Head') or ch:FindFirstChild('LowerTorso') or getClosestBodyPart(ch)
end

local function getAimPart(pl)
	local AA=Config['Aim Assist']
	local ch=pl.Character
	if not ch or not ch.Parent then return nil end
	local hum=ch:FindFirstChildOfClass('Humanoid')
	if not hum or hum.Health<=0 then return nil end
	return aimHitPart(AA,ch)
end

-- // [重写] 多点命中: 锁定之后, 用光标相对目标屏幕位置的偏移, 实时在目标身体上选瞄准点 //
-- // 上下左右移动鼠标就能在头/胸/腿之间来回切, 不需要重新锁定目标 //
local function aimPointFor(part,AA)
	local pos=part.Position
	local mp=tonumber(AA.Multipoint) or 0
	if mp<=0 then return pos end
	local ok,np=pcall(function()
		local center=aimCenter()
		local sp=Camera:WorldToViewportPoint(pos)
		local dist=math.max((Camera.CFrame.Position-pos).Magnitude,1)
		local pps=Camera.ViewportSize.Y/(2*math.tan(math.rad(Camera.FieldOfView)/2)*dist)
		if (not pps) or pps<=0.001 then pps=0.001 end
		local s=part.Size
		local halfX=(s.X*0.5)*(mp/100)
		local halfY=(s.Y*0.5)*(mp/100)
		local ox=math.clamp((center.X-sp.X)/pps,-halfX,halfX)
		local oy=math.clamp((sp.Y-center.Y)/pps,-halfY,halfY)
		return pos+Camera.CFrame.RightVector*ox+Vector3.new(0,oy,0)
	end)
	if ok and np then return np end
	return pos
end

-- // [重写] 预测: 水平/垂直滑块就是真正的预测秒数(不再被写死), AutoPrediction 再叠加 ping 补偿 //
local function predictedPos(part,pos,AA)
	local vel=partVelocity(part)
	local hp=tonumber(AA.HPrediction) or 0
	local vp=tonumber(AA.VPrediction) or 0
	if AA.AutoPrediction~=false then
		local ping=serverPing()
		hp=hp+ping/500
		vp=vp+ping/2000
	end
	if AA.DontAimVertically then vp=0 end
	local ny=vel.Y*vp
	local jp=tonumber(AA.JumpPredictionValue) or 0
	if AA.JumpPrediction and jp>0 and math.abs(vel.Y)>1 then
		local g=196.2
		local peak=vel.Y/g
		local new=0
		if jp<=peak then new=vel.Y*jp-0.5*g*jp^2
		else
			local fall=jp-peak
			local peakY=(vel.Y*peak)-0.5*g*peak^2
			new=peakY-0.5*g*fall^2
		end
		ny=new
	end
	return pos+Vector3.new(vel.X*hp,ny,vel.Z*hp)+Vector3.new(0,AA.JumpOffset or 0,0)
end

-- // [重写] FOV / 隔墙 / 中心点 只看瞄准辅助自己的设置 //
local function aimFovRadius()
	local AA=Config['Aim Assist']
	if AA.Enabled and AA.UseFOV and bindActive('Aim Assist') then return math.max((AA.FOVSize or 600)/2,1) end
	return 0
end
local function aimWallCheck()
	return Config['Aim Assist'].WallCheck==true
end
-- // [修复] FOV 中心点: 默认锁死屏幕中心; 打开"FOV跟随鼠标光标"后跟着真实光标走 //
function aimCenter()
	local AA=Config['Aim Assist']
	-- // [修复] “FOV跟随鼠标光标”: 始终取自跟踪的光标位置 (游戏内指针被LockCenter锁定, GetMouseLocation恒为定点) //
	if AA.FOVMouse then
		local okMB,mb=pcall(function() return UserInputService.MouseBehavior end)
		if okMB and mb and mb~=Enum.MouseBehavior.Default then return Vector2.new(Camera.ViewportSize.X/2,Camera.ViewportSize.Y/2) end
		if mouseCursorPos then return mouseCursorPos end
		local ok,ml=pcall(function() return UserInputService:GetMouseLocation() end)
		if ok and ml then return ml end
	end
	return Vector2.new(Camera.ViewportSize.X/2,Camera.ViewportSize.Y/2)
end
local function passesTargetCheck(pl,part,pos,dist,onScreen)
	local AA=Config['Aim Assist']
	if not onScreen then return false end
	local md=AA.MaxDistance or 0
	if md>0 then
		local my=LocalPlayer.Character and LocalPlayer.Character:FindFirstChild('HumanoidRootPart')
		if my and (pos-my.Position).Magnitude>md then return false end
	end
	local fovr=aimFovRadius()
	if fovr>0 and dist>fovr then return false end
	if aimWallCheck() and not isPartVisible(part) then return false end
	return true
end

function selectAimbotTarget(force)
	local AA=Config['Aim Assist']
	local center=aimCenter()
	if not force and AA.Sticky and aimbotTargetPlayer and aimbotTargetPart and aimbotTargetPart.Parent then
		local pl=aimbotTargetPlayer
		local part=getAimPart(pl)
		if part and not isWhitelisted(pl) and not isPlayerKnockedOrKO(pl) then
			-- // [修复] 粘住目标以后也要每帧重新过一遍 FOV/隔墙/距离, 否则锁定后这些条件就再也没生效过 //
			local pos=aimPointFor(part,AA)
			local sp,on=Camera:WorldToViewportPoint(pos)
			local d=on and (Vector2.new(sp.X,sp.Y)-center).Magnitude or math.huge
			if on and passesTargetCheck(pl,part,pos,d,on) then
				stickyFailTime=0
				aaStatusFound=1;aaStatusDist=d
				return pl,part
			end
			-- // [修复] 失锁 0.25s 宽限: 单帧被墙挡一下/抖动/FOV边缘, 不立刻放掉锁定 //
			if stickyFailTime==0 then stickyFailTime=tick() end
			if tick()-stickyFailTime<0.25 then
				aaStatusFound=1;aaStatusDist=d
				return pl,part
			end
		end
		aimbotTargetPlayer=nil;aimbotTargetPart=nil;stickyFailTime=0
	end
	stickyFailTime=0
	local best,bestPart,bestD=nil,nil,math.huge
	local found=0
	for _,pl in ipairs(getValidTargetPlayers()) do
		found=found+1
		local part=getAimPart(pl)
		if part then
			local pos=aimPointFor(part,AA)
			local sp,on=Camera:WorldToViewportPoint(pos)
			if on then
				local d=(Vector2.new(sp.X,sp.Y)-center).Magnitude
				if d<bestD and passesTargetCheck(pl,part,pos,d,on) then bestD=d;best=pl;bestPart=part end
			end
		end
	end
	aaStatusFound=found
	aaStatusDist=(bestD<1e8) and bestD or 0
	return best,bestPart
end

-- // [已删除] Target Bind / 锁定目标键: 和"瞄准辅助(绑定按键)"完全重复, 统一由主开关控制 //

function restoreAimCamera()
	aimCamActive=false
	pcall(function() if Camera.CameraType~=Enum.CameraType.Custom then Camera.CameraType=Enum.CameraType.Custom end end)
end

local function aimCameraLerp(pos,a)
	if not a or a<=0 then a=0.01 end
	pcall(function()
		local cf=Camera.CFrame
		local d=pos-cf.Position
		if d.Magnitude<0.5 then return end
		Camera.CFrame=cf:Lerp(CFrame.new(cf.Position,cf.Position+d.Unit),math.clamp(a,0.001,1))
	end)
end

function updateAimFOV()
	if not aaFovCircle then return end
	local AA=Config['Aim Assist']
	-- // [修复] FOV圈与辅助瞄准开关解耦: 只要“启用FOV+显示FOV”开着就一直生效, 无需在UI重新开关 //
	local show=Started and not PanicMode and not Unloaded and AA.UseFOV and AA.FOVVisible
	if show then
		local pos=aimCenter()
		aaFovCircle.Visible=true;aaFovCircle.Position=pos;aaFovCircle.Radius=math.max((AA.FOVSize or 600)/2,1)
		aaFovCircle.Thickness=AA.FOVThickness or 1.5;aaFovCircle.Color=AA.FOVColor or Color3.fromRGB(138,110,255)
		aaFovCircle.Filled=false
	else aaFovCircle.Visible=false end
	pcall(function() fovCircle.Visible=false end)
	-- // 实时显示当前瞄准目标 (0.25s 刷一次, 不每帧刷 UI) //
	if aaStatus and tick()>=aaStatusNext then
		aaStatusNext=tick()+0.25
		pcall(function() aaStatus:Refresh() end)
	end
end

-- // [重写] 瞄准辅助核心: 不再把 CameraType 改成 Scriptable //
-- // da hood 自己的相机脚本每帧都会重写 Camera.CFrame, 之前改成 Scriptable 后两边互相覆盖 -> 辅助瞄准完全没反应 //
-- // 现在按 juju 做法: 本脚本的 RenderStepped 跑在游戏相机脚本之后, 直接对 CFrame 做 Lerp 就能生效 //
-- // [重映射] 平滑度: 1=彻底锁死(准星一动不动), 数值越大越平滑 //
-- // 旧公式最猛也只有约 25%/帧, 所以拉到 1 也永远锁不死 //
local function smoothAlpha(v,dt)
	-- // [重映射] 1-20: 1-5 硬锁, 5-10 微硬锁, 10-15 微软锁, 15-20 软锁; 1 = 彻底锁死(准星瞬间贴目标) //
	local s=tonumber(v) or 10
	if s<=1 then return 1 end
	local t=math.clamp((s-1)/19,0,1)
	local a=1-t*0.95
	return math.clamp(a,0.05,1)
end
local function aimSmoothAA(AA,dt)
	local aH=smoothAlpha(AA.HSmoothness,dt)
	local aV=smoothAlpha(AA.VSmoothness,dt)
	if AA.SmoothStyle=='Uniform' then
		local m=math.min(aH,aV)
		aH=m;aV=m
	end
	return aH,aV
end
function applyAimbotImpl(dt)
	local AA=Config['Aim Assist']
	if not (AA.Enabled and bindActive('Aim Assist')) then
		aimbotTargetPlayer=nil;aimbotTargetPart=nil;aimAssistPart=nil
		if aimCamActive then restoreAimCamera() end
		if aaFovCircle then aaFovCircle.Visible=false end
		return
	end
	if isSelfKnocked() then
		aimAssistPart=nil
		if aimCamActive then restoreAimCamera() end
		return
	end
	local now=tick()
	local selDelay=math.max(AA.AutoSelectDelay or 0.03,0.005)
	local need=(not aimbotTargetPlayer) or (not aimbotTargetPart) or (not aimbotTargetPart.Parent)
	if need or (AA.AutoSelect and now-aimbotLastSelect>=selDelay) then
		aimbotLastSelect=now
		local pl,part=selectAimbotTarget(false)
		aimbotTargetPlayer=pl;aimbotTargetPart=part
	end
	local pl=aimbotTargetPlayer
	if not pl then
		aimAssistPart=nil
		if aimCamActive then restoreAimCamera() end
		return
	end
	-- // [修复] 命中部位每帧重新解析: 改命中部位/空中落地都立刻生效, 不用重新锁一次目标 //
	local fresh=getAimPart(pl)
	if fresh then aimbotTargetPart=fresh end
	local part=aimbotTargetPart
	if not part or not part.Parent then
		aimAssistPart=nil;aimbotTargetPlayer=nil
		if aimCamActive then restoreAimCamera() end
		return
	end
	-- // [修复] 隔墙不瞄: 粘住目标之后同样要每帧复检 //
	if aimWallCheck() and not isPartVisible(part) then
		aimAssistPart=part
		if aimCamActive then restoreAimCamera() end
		return
	end
	aimAssistPart=part
	local pos=predictedPos(part,aimPointFor(part,AA),AA)
	local aH,aV=aimSmoothAA(AA,dt)
	local canMouse=(type(mousemoverel)=="function") or (type(setmouseposition)=="function")
	local done=false
	local okMB,mb2=pcall(function() return UserInputService.MouseBehavior end)
	local mouseLocked=okMB and mb2~=nil and mb2~=Enum.MouseBehavior.Default
	-- // [修复] 锁定视角时鼠标被钉在屏幕中心, 再调 mousemoverel 会和游戏自己的视角控制打架, 鼠标左右乱滑 //
	-- // // 锁定模式直接走下面的相机 lerp: 第一人称里相机就是准星, 效果等同鼠标锁住人物ESP //
	if AA.Style=='Mouse' and canMouse and not mouseLocked then
		local sp,on=Camera:WorldToViewportPoint(pos)
		if on then
			-- // [修复] 始终用真实鼠标位置做基准 (juju: distance = new_pos - mouse_position) //
			-- // 第3人称不锁视角时若用屏幕中心做基准, 鼠标会朝错误方向飘 //
			local cur
			local okML,ml=pcall(function() return UserInputService:GetMouseLocation() end)
			if okML and ml then cur=ml
			elseif mouseCursorPos then cur=mouseCursorPos
			else cur=Vector2.new(Camera.ViewportSize.X/2,Camera.ViewportSize.Y/2) end
			local dx=(sp.X-cur.X)*aH
			local dy=(AA.DontAimVertically and 0 or (sp.Y-cur.Y)*aV)
			if type(mousemoverel)=="function" then
				done=pcall(function() mousemoverel(dx,dy) end)
			else
				done=pcall(function() setmouseposition(cur.X+dx,cur.Y+dy) end)
			end
		end
	end
	if not done then
		if AA.DontAimVertically then pos=Vector3.new(pos.X,Camera.CFrame.Position.Y,pos.Z) end
		aimCameraLerp(pos,aH)
	end
end
-- // [修复] BindToRenderStep 绑定的函数只要报错一次就会永久停止运行, 之前目标死亡/倒地瞬间 part 被销毁, 一次报错就让辅助瞄准突然失灵 //
-- // 外面再包一层 pcall: 出错时清掉锁定状态并恢复相机, 下一帧自动恢复 //
function applyAimbot(dt)
	local ok=pcall(applyAimbotImpl,dt)
	if not ok then
		aimbotTargetPlayer=nil;aimbotTargetPart=nil;aimAssistPart=nil
		stickyFailTime=0
		if aimCamActive then restoreAimCamera() end
		if aaFovCircle then aaFovCircle.Visible=false end
	end
end
-- // [修复] 把"应用瞄准"挂到相机优先级之后: 游戏自己的相机脚本用 BindToRenderStep(RenderPriority.Camera) //
-- // 每帧重写 Camera.CFrame, 挂在普通 RenderStepped 里的写入会被它盖掉 -> 看起来"锁上了但镜头不动" //
pcall(function()
	RunService:BindToRenderStep("HateCC_AimApply",Enum.RenderPriority.Camera.Value+10,function(dt)
		if Unloaded or not Started then return end
		applyAimbot(dt)
	pcall(updateAimFOV) -- // [修复] FOV圈更新必须晚于瞄准应用(Camera+10), 否则会被早退分支再次隐藏 //
	end)
	aimApplyBound=true
end)


-- ######################## 假同步 (free Desync + Velocity/Network/RandomTP 合并) ########################
-- ######################## 假同步 (free 逻辑: 视角不变 + 真身眼睛 + 英文状态) ########################
desyncSetback=nil
desyncEye=nil
desyncEyePupil=nil
desyncStatus=nil
local function projectClamped(pos)
	local vp=Camera.ViewportSize
	local p,on=Camera:WorldToViewportPoint(pos)
	if on then return Vector2.new(p.X,p.Y) end
	local center=Vector2.new(vp.X/2,vp.Y/2)
	local d=Vector2.new(p.X-center.X,p.Y-center.Y)
	local m=d.Magnitude
	if m<1 then return center end
	d=d/m
	return center+d*(math.min(vp.X,vp.Y)/2-40)
end
function toggleDesync(state)
	Config['Desync'].Enabled=state
	if state then
		local hrp=LocalPlayer.Character and LocalPlayer.Character:FindFirstChild('HumanoidRootPart')
		if not desyncSetback then
			desyncSetback=Instance.new("Part"); desyncSetback.Name="Desync Setback"; desyncSetback.Parent=Workspace; desyncSetback.Size=Vector3.new(2,2,1); desyncSetback.CanCollide=false; desyncSetback.Anchored=true; desyncSetback.Transparency=1
		end
		desyncSetback.CFrame=(hrp and (hrp.CFrame*CFrame.new(0,2.5,0))) or CFrame.new()
		Camera.CameraSubject=desyncSetback
	else
		desyncRestoreView()
		if desyncEye then desyncEye.Visible=false;if desyncEyePupil then desyncEyePupil.Visible=false end end
	end
	notifyToggle("Desync",state)
	refreshAllComponents()
	updateKeybindDisplay()
end

-- // [优化] 移动判定: 只有"动起来"假同步才生效, 站着不动=原地传送 //
desyncMoving=false
-- // [修复] 相机锚点: 永远停在"真身"当前位置, 保证视角和没开假同步时一模一样 //
function desyncAnchorCF(hrp,cf)
	return cf*CFrame.new(0,2.5,0)
end
function desyncRestoreView()
	if Camera.CameraSubject==desyncSetback then
		local hum=LocalPlayer.Character and LocalPlayer.Character:FindFirstChildOfClass('Humanoid')
		pcall(function() Camera.CameraSubject=hum or LocalPlayer.Character or Camera.CameraSubject end)
	end
end

local function checkMoving(hum,hrp)
	local md=hum and hum.MoveDirection or Vector3.new()
	if md.Magnitude>0.05 then return true end
	local v=hrp.AssemblyLinearVelocity
	if typeof(v)~="Vector3" then v=hrp.Velocity or Vector3.new() end
	if math.abs(v.Y)>1 or Vector3.new(v.X,0,v.Z).Magnitude>1 then return true end
	for _,kn in ipairs({'W','A','S','D'}) do
		local ok,kc=pcall(function() return Enum.KeyCode[kn] end)
		if ok and kc and UserInputService:IsKeyDown(kc) then return true end
	end
	return false
end

task.spawn(function()
	while task.wait(0) do
		if Unloaded or not Started then desyncRestoreView() continue end
		local DS=Config['Desync']
		local ch=LocalPlayer.Character
		local hrp=ch and ch:FindFirstChild('HumanoidRootPart')
		if not DS.Enabled then
			desyncRestoreView()
			desyncActiveThisFrame=false;desyncMoving=false;desyncFakePos=nil
			if desyncStatus then desyncStatus.Visible=false end
			if desyncEye then desyncEye.Visible=false;if desyncEyePupil then desyncEyePupil.Visible=false end end
			continue
		end
		if not hrp then desyncRestoreView() continue end
		local hum=ch:FindFirstChildOfClass('Humanoid')
		desyncActiveThisFrame=true
		if not desyncStatus then
			desyncStatus=Drawing.new("Text");desyncStatus.Size=14;desyncStatus.Font=2;desyncStatus.Outline=true;desyncStatus.OutlineColor=Color3.new(0,0,0);desyncStatus.Visible=false
		end
		if not desyncSetback or not desyncSetback.Parent then
			desyncSetback=Instance.new("Part"); desyncSetback.Name="Desync Setback"; desyncSetback.Parent=Workspace; desyncSetback.Size=Vector3.new(2,2,1); desyncSetback.CanCollide=false; desyncSetback.Anchored=true; desyncSetback.Transparency=1
		end
		local old=hrp.CFrame
		-- // [修复A] 人物是一整个装配体, 写已废弃的 .Velocity 在根部件上不生效 -> "速度假同步"毫无反应 //
		local oldVel=hrp.AssemblyLinearVelocity
		if typeof(oldVel)~="Vector3" then oldVel=hrp.Velocity or Vector3.new() end
		-- // [修复B] 先把相机锚点对齐真身本帧位置, 再制造假位置 -> 视角不会被假位置甩出去 //
		desyncSetback.CFrame=desyncAnchorCF(hrp,old)
		Camera.CameraSubject=desyncSetback
		desyncMoving=checkMoving(hum,hrp)
		local moveOK=(not DS.MoveOnly) or desyncMoving
		local fakePos=old.Position
		local fakeVel=nil
		if DS.Mode=='Underground' then
			if moveOK then fakePos=old.Position-Vector3.new(0,12+(DS.Depth or 0),0) end
		elseif DS.Mode=='Void' then
			if moveOK then local r=math.floor(DS.HOffset*40+200) fakePos=old.Position+Vector3.new(math.random(-r,r),math.random(-r,r),math.random(-r,r)) end
		end
		if DS.Velocity and moveOK then
			local vmode=DS.VelocityValue
			-- // [修复C] DS.Random*5.5 是小数, 丢进 math.random 会抛 "number has no integer representation", //
			-- // 整个假同步线程当场死掉 -> 表现就是"速度假同步完全无法使用" //
			local r=math.max(math.floor((DS.Random or 5)*5.5),1)
			if vmode=='Zero' then fakeVel=Vector3.new()
			elseif vmode=='Max' then fakeVel=Vector3.new(63536,63536,63536)
			elseif vmode=='Sky' then fakeVel=Vector3.new(0,10000,0)
			elseif vmode=='Underground' then fakeVel=Vector3.new(0,-10000,0)
			elseif vmode=='Multiplier' then fakeVel=oldVel*(DS.Multiplier or 0.2)
			else fakeVel=Vector3.new(math.random(-r,r),math.random(-r,r),math.random(-r,r)) end
		end
		if DS.Network and moveOK then
			local nvmode=DS.NetworkValue
			local r=math.max(math.floor((DS.Random or 5)*3277),1024)
			if nvmode=='Invisible' then
				sflag('S2PhysicsSenderRate','2');sflag('PhysicsSenderMaxBandwidthBps','1.047');shp(hrp,'NetworkIsSleeping',doSleep)
				fakeVel=Vector3.new(math.random(-r,r),math.random(-r,r),math.random(-r,r))
			elseif nvmode=='Lag step' then
				sflag('S2PhysicsSenderRate','1');shp(hrp,'NetworkIsSleeping',doSleep);shp(hrp,'NetworkIsSleeping',not doSleep);shp(hrp,'NetworkIsSleeping',doSleep)
				fakeVel=Vector3.new(0,0,0)
			elseif nvmode=='Random' then
				sflag('S2PhysicsSenderRate',math.random(1,15)==1 and '6' or '1')
				fakeVel=Vector3.new(math.random(-r,r),math.random(-r,r),math.random(-r,r))
				shp(hrp,'NetworkIsSleeping',doSleep)
			elseif nvmode=='Teleport move' then
				shp(hrp,'NetworkIsSleeping',doSleep);sflag('S2PhysicsSenderRate','1000');shp(hrp,'NetworkIsSleeping',false);shp(hrp,'NetworkIsSleeping',true);shp(hrp,'NetworkIsSleeping',false)
			else
				shp(hrp,'NetworkIsSleeping',doSleep)
			end
			doSleep=not doSleep
		end
		if DS.RandomTeleport and moveOK then
			local ho=math.max(math.floor(DS.HOffset),1);local vo=math.max(math.floor(DS.VOffset),1)
			fakePos=old.Position+Vector3.new(math.random(-ho,ho),math.random(-vo,vo),math.random(-ho,ho))
		end
		-- // [修复] 传送时保留原有朝向, 避免人物被拧正之后看起来在乱转 //
		local keepRot=old-old.Position
		hrp.CFrame=CFrame.new(fakePos)*keepRot
		if fakeVel then pcall(function() hrp.AssemblyLinearVelocity=fakeVel end) end
		desyncFakePos=fakePos
		RunService.RenderStepped:Wait()
		-- // [修复D] 核心: 不管开的是哪一种假同步, 一帧之后都必须把真身的"位置+速度"成对还原. //
		-- // 旧代码只在"速度假同步"打开时还原速度, 网络假同步写进去的随机巨速留在人物上, //
		-- // 下一帧物理引擎真的把人甩出去 -> 人物顶飞/乱飞, 相机跟着一起飞 //
		pcall(function() hrp.CFrame=old end)
		pcall(function() hrp.AssemblyLinearVelocity=oldVel end)
		if desyncSetback then desyncSetback.CFrame=desyncAnchorCF(hrp,old) end
		if DS.ShowEye then
			local size=DS.EyeSize or 14
			local color=DS.EyeColor or Color3.new(1,1,1)
			if not desyncEye then
				desyncEye=Drawing.new("Circle");desyncEye.Filled=true;desyncEye.NumSides=24;desyncEye.Thickness=2;desyncEye.Visible=false
				desyncEyePupil=Drawing.new("Circle");desyncEyePupil.Filled=true;desyncEyePupil.NumSides=16;desyncEyePupil.Color=Color3.new(0,0,0);desyncEyePupil.Visible=false
			end
			desyncEye.Radius=size;desyncEye.Color=color
			desyncEyePupil.Radius=size*0.4
			local p=projectClamped(desyncFakePos or hrp.Position)
			desyncEye.Position=p;desyncEye.Visible=true
			desyncEyePupil.Position=p;desyncEyePupil.Visible=true
		else
			if desyncEye then desyncEye.Visible=false;desyncEyePupil.Visible=false end
		end
		local mv=moveOK and "MOVING" or "IDLE"
		desyncStatus.Text="Desync: ON ("..mv..")"
		desyncStatus.Color=moveOK and Color3.fromRGB(120,255,120) or Color3.fromRGB(255,200,90)
		desyncStatus.Position=Vector2.new(15,15)
		desyncStatus.Visible=true
	end
end)


-- // [修复] Ragebot 自动踩踏 (juju 式独立循环: 扫描 ragebot 目标里被击倒且未死者, 踩完传送回来) //
local stompLastFire=0
track(RunService.Heartbeat:Connect(function()
	if Unloaded or not Started then return end
	local RB=Config.Ragebot
	if not (RB.Enabled and bindActive('Ragebot') and RB.AutoStomp) then
		ragebotBackPos=nil
		return
	end
	local ch=LocalPlayer.Character if not ch then return end
	local hrp=ch:FindFirstChild('HumanoidRootPart') if not hrp then return end
	local stompT=nil
	for _,uid in ipairs(RB.Targets or {}) do
		local p=Players:GetPlayerByUserId(uid)
		if p and p~=LocalPlayer and p.Character then
			local pbe=p.Character:FindFirstChild(GameCfg.folderName)
			local pko=pbe and (pbe:FindFirstChild(GameCfg.knocked) or pbe:FindFirstChild('K.O') or pbe:FindFirstChild('Knocked'))
			local psd=pbe and pbe:FindFirstChild('SDeath')
			if pko and pko.Value and not (psd and psd.Value) then stompT=p break end
		end
	end
	if not stompT and ragebotTarget and ragebotTarget~=LocalPlayer and ragebotTarget.Character then
		local pbe=ragebotTarget.Character:FindFirstChild(GameCfg.folderName)
		local pko=pbe and (pbe:FindFirstChild(GameCfg.knocked) or pbe:FindFirstChild('K.O') or pbe:FindFirstChild('Knocked'))
		local psd=pbe and pbe:FindFirstChild('SDeath')
		if pko and pko.Value and not (psd and psd.Value) then stompT=ragebotTarget end
	end
	if stompT then
		if not ragebotBackPos then ragebotBackPos=hrp.CFrame end
		local ut=stompT.Character:FindFirstChild('UpperTorso') or stompT.Character:FindFirstChild('HumanoidRootPart')
		if ut then hrp.CFrame=CFrame.new(ut.Position+Vector3.new(0,3,0)) end
		if tick()-stompLastFire>0.03 then
			stompLastFire=tick()
			local ev=getMainEvent()
			if ev then pcall(function() ev:FireServer('Stomp') end) end
		end
	elseif ragebotBackPos then
		if RB.TeleportBack then pcall(function() hrp.CFrame=ragebotBackPos end) end
		ragebotBackPos=nil
	end
end))


-- ######################## Feature Indicators (juju 移植: 右侧热键状态指示) ########################
indicatorGradientData=""
pcall(function()
	if crypt and crypt.base64 and crypt.base64.decode then
		indicatorGradientData=crypt.base64.decode("iVBORw0KGgoAAAANSUhEUgAAAGkAAAAhCAYAAADaiYU7AAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAJcEhZcwAADsMAAA7DAcdvqGQAAACySURBVGhD7dFBCsMwDABBtbSP8v8P+Yu/kBwahRqMiO9Z2AEjozinffXeY9u2T0R8zzNmqrs6V+/S6p8x6264e1vnfE/z9+o4z/6fadxzzvfVHOr+7u0802pX96t31661dryvlR7NSABGAjASgJEAjARgJAAjARgJwEgARgIwEoCRAIwEYCQAIwEYCcBIAEYCMBKAkQCMBGAkACMBGAnASABGAjASgJEAjARgJAAjPV7ED23xMgBp5elFAAAAAElFTkSuQmCC")
	end
end)
kdSig=nil;kdRows={};kdBounds=nil;indicatorDragged=false
function updateKeybindDisplay()
	local VA=Config['Visual Awareness']
	local show=VA.KeybindDisplay and (not Unloaded) and (not PanicMode) and Started
	if not show then
		if kdSig~=nil then
			for _,o in pairs(keybindDisplayObjects) do pcall(function() o:Remove() end) end
			keybindDisplayObjects={};kdRows={};kdSig=nil;kdBounds=nil;kdLayout=nil
		end
		return
	end
	local size=VA.KeybindDisplaySize or 12
	local font=FONTMAP[VA.KeybindDisplayFont] or 0
	local vp=Camera.ViewportSize
	local right=(VA.KeybindDisplayPos=='Right')
	-- // 列出所有『可以绑定按键』的功能 (未绑定也显示, 绑定并开启后变紫色) //
	local names={'UI Toggle'}
	for _,n in ipairs(BIND_ORDER) do table.insert(names,n) end

	local sig=table.concat(names,'|')..'@'..size..'@'..tostring(font)
	if sig~=kdSig then
		for _,o in pairs(keybindDisplayObjects) do pcall(function() o:Remove() end) end
		keybindDisplayObjects={};kdRows={};kdSig=sig;kdLayout=nil
		for i,n in ipairs(names) do
			local bg=Drawing.new("Square");bg.Filled=true;bg.Transparency=0.28;bg.Color=Color3.fromRGB(6,6,8);bg.Visible=true;bg.ZIndex=1
			local bar=Drawing.new("Square");bar.Filled=true;bar.Transparency=0;bar.Color=Color3.fromRGB(38,38,48);bar.Visible=true;bar.ZIndex=2
			local tx=Drawing.new("Text");tx.Font=font;tx.Size=size;tx.Outline=true;tx.OutlineColor=Color3.new(0,0,0);tx.Center=false;tx.Visible=true;tx.ZIndex=3
			table.insert(keybindDisplayObjects,bg);table.insert(keybindDisplayObjects,bar);table.insert(keybindDisplayObjects,tx)
			kdRows[i]={name=n,bg=bg,bar=bar,tx=tx}
		end
	end
	if #kdRows==0 then
		local tx=Drawing.new("Text");tx.Font=font;tx.Size=size;tx.Outline=true;tx.Text="[ ]  "..T("NoBinds");tx.Color=Color3.fromRGB(120,120,135);tx.Visible=true;tx.ZIndex=3
		table.insert(keybindDisplayObjects,tx)
		table.insert(kdRows,{name='__none__',tx=tx})
	end
	local onCol=(UI and UI.Accent) or Color3.fromRGB(124,110,255)
	local offCol=VA.KeybindDisplayColor or Color3.new(1,1,1)
	local rowH=size+11;local gap=3;local maxW=150
	for _,r in ipairs(kdRows) do
		if r.name=='__none__' then
			r.w=r.tx.TextBounds.X+28
		else
			local act
			if r.name=='UI Toggle' then act=GuiOpen==true else act=bindFeatureActive(r.name) end
			r.active=act
			local d=BIND_DEFS[r.name]
			local kn=getBindKey(Config.Keybinds[r.name]);r.bound=(kn~=nil and kn~='')
			r.tx.Text='['..((r.bound and kn) or '--')..']  '..((d and d.Label) or r.name)
			r.tx.Color=act and onCol or (r.bound and offCol or Color3.fromRGB(math.floor(offCol.R*180),math.floor(offCol.G*180),math.floor(offCol.B*180)))
			r.w=r.tx.TextBounds.X+34
		end
		if r.bar then r.bar.Color=(r.name=='__none__') and Color3.fromRGB(38,38,48) or (r.active and onCol or Color3.fromRGB(38,38,48)) end
		if r.w>maxW then maxW=r.w end
	end
	local perCol=math.clamp(#kdRows,1,8)
	-- // [修复] 拖动过程中冻结面板宽度, 免得文字宽度每帧微抖动导致整块左右跳 //
	if indicatorDragging and kdLayout then maxW=kdLayout.maxW end
	local cols=math.ceil(#kdRows/perCol)
	local totalW=cols*maxW+(cols-1)*gap
	kdLayout={maxW=maxW,rowH=rowH,gap=gap,perCol=perCol,cols=cols,totalW=totalW}
	local x=indicatorPos.X;local y=indicatorPos.Y
	if not indicatorDragged then
		x=(right and (vp.X-totalW-15)) or 15;y=72
	end
	moveIndicatorTo(x,y)
end

-- // ============================================================ //
-- // [整合模块] 粒子光环(合并) / 力场身体/帽子 / Hitsounds / UI  //
-- // ============================================================ //

-- ######################## 粒子光环 (juju 粒子 + free Aura 合并) ########################
auraPart=nil
auraEmitters={}
local function buildAuraEmitters(selected)
	for _,e in pairs(auraEmitters) do pcall(function() e:Destroy() end) end
	auraEmitters={}
	local A=Config['Local Player Visuals']
	if not A.ParticleAura then return end
	if not auraPart then
		auraPart=Instance.new("Part"); auraPart.Name="HateAura"; auraPart.Size=Vector3.new(0.01,0.01,0.01); auraPart.Transparency=1; auraPart.CanCollide=false; auraPart.Anchored=true; auraPart.Parent=Workspace
	end
	auraPart.Size=(selected=='Rain') and Vector3.new(5,0.01,5) or Vector3.new(0.01,0.01,0.01)
	local function make(props)
		local e=Instance.new("ParticleEmitter")
		for k,v in pairs(props) do e[k]=v end
		e.Parent=auraPart
		auraEmitters[#auraEmitters+1]=e
	end
	local cs=ColorSequence.new(A.ParticleAuraColor)
	if selected=="Swirl" then
		make({Texture="rbxassetid://8047533775",Color=cs,Lifetime=NumberRange.new(1,1),Rate=10,LightEmission=0.4,LockedToPart=true,Orientation=Enum.ParticleOrientation.VelocityPerpendicular,RotSpeed=NumberRange.new(200,400),Rotation=NumberRange.new(-180,180),Speed=NumberRange.new(3,6),SpreadAngle=Vector2.new(10,-10),Size=NumberSequence.new{NumberSequenceKeypoint.new(0,3,0),NumberSequenceKeypoint.new(0.64,2,0),NumberSequenceKeypoint.new(1,0.75,0)},Transparency=NumberSequence.new{NumberSequenceKeypoint.new(0,1,0),NumberSequenceKeypoint.new(0.28,0,0),NumberSequenceKeypoint.new(0.7,0,0),NumberSequenceKeypoint.new(1,1,0)}})
		make({Texture="rbxassetid://8047796070",Color=cs,Lifetime=NumberRange.new(1,1),Rate=10,LightEmission=1,LockedToPart=true,Orientation=Enum.ParticleOrientation.VelocityPerpendicular,RotSpeed=NumberRange.new(100,300),Rotation=NumberRange.new(-180,180),Speed=NumberRange.new(3,5),SpreadAngle=Vector2.new(10,-10),Size=NumberSequence.new{NumberSequenceKeypoint.new(0,3.1,0),NumberSequenceKeypoint.new(0.42,1.4,0),NumberSequenceKeypoint.new(1,0.94,0)},Transparency=NumberSequence.new{NumberSequenceKeypoint.new(0,1,0),NumberSequenceKeypoint.new(0.23,0.03,0),NumberSequenceKeypoint.new(0.63,0.26,0),NumberSequenceKeypoint.new(1,1,0)}})
	elseif selected=="Bubble" then
		make({Texture="rbxassetid://1084955012",Color=cs,Lifetime=NumberRange.new(0.33,0.33),Rate=12,LightEmission=1,LockedToPart=true,Rotation=NumberRange.new(-180,180),Speed=NumberRange.new(0,0),Size=NumberSequence.new{NumberSequenceKeypoint.new(0,4.8,0),NumberSequenceKeypoint.new(1,4.8,0)},Transparency=NumberSequence.new{NumberSequenceKeypoint.new(0,0.88,0),NumberSequenceKeypoint.new(0.5,0.4,0),NumberSequenceKeypoint.new(1,0.88,0)}})
		make({Texture="rbxassetid://1084955488",Color=cs,Lifetime=NumberRange.new(1,1),Rate=6,LightEmission=1,LockedToPart=true,Rotation=NumberRange.new(-180,180),Speed=NumberRange.new(0,0),Size=NumberSequence.new{NumberSequenceKeypoint.new(0,4,0),NumberSequenceKeypoint.new(1,4,0)},Transparency=NumberSequence.new{NumberSequenceKeypoint.new(0,1,0),NumberSequenceKeypoint.new(0.5,0.7,0),NumberSequenceKeypoint.new(1,1,0)}})
	elseif selected=="Air" then
		make({Texture="rbxassetid://10558425570",Color=cs,Lifetime=NumberRange.new(2,2),Rate=75,LightEmission=1,LockedToPart=true,Orientation=Enum.ParticleOrientation.VelocityParallel,RotSpeed=NumberRange.new(200,200),ShapeInOut=Enum.ParticleEmitterShapeInOut.InAndOut,Speed=NumberRange.new(0.01,0.01),SpreadAngle=Vector2.new(-360,360),Squash=NumberSequence.new(0),Size=NumberSequence.new{NumberSequenceKeypoint.new(0,7,0),NumberSequenceKeypoint.new(1,7,0)},Transparency=NumberSequence.new{NumberSequenceKeypoint.new(0,1,0),NumberSequenceKeypoint.new(0.5,0.93,0),NumberSequenceKeypoint.new(1,1,0)},ZOffset=-1})
	elseif selected=="Ritual" then
		make({Texture="rbxassetid://564938805",Color=cs,Lifetime=NumberRange.new(1,1),Rate=1,LightEmission=1,LockedToPart=true,Orientation=Enum.ParticleOrientation.VelocityPerpendicular,RotSpeed=NumberRange.new(360,360),Speed=NumberRange.new(0.001,0.001),Size=NumberSequence.new{NumberSequenceKeypoint.new(0,5,0),NumberSequenceKeypoint.new(1,5,0)},Transparency=NumberSequence.new{NumberSequenceKeypoint.new(0,1,0),NumberSequenceKeypoint.new(0.1,0,0),NumberSequenceKeypoint.new(0.83,0,0),NumberSequenceKeypoint.new(1,1,0)}})
	elseif selected=="Rain" then
		make({Texture="rbxassetid://419625073",Color=cs,Lifetime=NumberRange.new(200,200),Rate=100,LightInfluence=1,EmissionDirection=Enum.NormalId.Bottom,Speed=NumberRange.new(25,25),Size=NumberSequence.new{NumberSequenceKeypoint.new(0,0.5,0),NumberSequenceKeypoint.new(1,0.5,0)},Transparency=NumberSequence.new{NumberSequenceKeypoint.new(0,0.5,0),NumberSequenceKeypoint.new(1,0.5,0)},VelocityInheritance=100})
	elseif selected=="Skibidi RedRizz" then
		make({Texture="rbxassetid://10558425570",Color=cs,Lifetime=NumberRange.new(2,2),Rate=40,LightEmission=10,LockedToPart=true,Orientation=Enum.ParticleOrientation.VelocityPerpendicular,RotSpeed=NumberRange.new(200,200),SpreadAngle=Vector2.new(-360,360),VelocitySpread=-360,Squash=NumberSequence.new(0),Speed=NumberRange.new(0.01,0.01),Size=NumberSequence.new{NumberSequenceKeypoint.new(0,7,0),NumberSequenceKeypoint.new(1,7,0)},Transparency=NumberSequence.new{NumberSequenceKeypoint.new(0,1,0),NumberSequenceKeypoint.new(0.5,0.5,0),NumberSequenceKeypoint.new(1,1,0)},ZOffset=-1,ShapeInOut=Enum.ParticleEmitterShapeInOut.InAndOut})
	elseif selected=="Bolts" then
		make({Texture="rbxassetid://1084955012",Color=cs,Lifetime=NumberRange.new(0.333,0.333),Rate=12,LightEmission=1,LockedToPart=true,Rotation=NumberRange.new(-180,180),Speed=NumberRange.new(0,0),Size=NumberSequence.new{NumberSequenceKeypoint.new(0,4.8,0),NumberSequenceKeypoint.new(1,4.8,0)},Transparency=NumberSequence.new{NumberSequenceKeypoint.new(0,0.88,0),NumberSequenceKeypoint.new(0.055,0.98,0),NumberSequenceKeypoint.new(0.111,0.17,0),NumberSequenceKeypoint.new(0.166,0.39,0),NumberSequenceKeypoint.new(0.222,0.12,0),NumberSequenceKeypoint.new(0.277,0.92,0),NumberSequenceKeypoint.new(0.333,0.41,0),NumberSequenceKeypoint.new(0.388,0.21,0),NumberSequenceKeypoint.new(0.444,0.78,0),NumberSequenceKeypoint.new(0.5,0.23,0),NumberSequenceKeypoint.new(0.555,0.78,0),NumberSequenceKeypoint.new(0.61,0.81,0),NumberSequenceKeypoint.new(0.666,0.91,0),NumberSequenceKeypoint.new(0.72,0.87,0),NumberSequenceKeypoint.new(0.777,0.41,0),NumberSequenceKeypoint.new(0.83,0.3,0),NumberSequenceKeypoint.new(0.888,0.16,0),NumberSequenceKeypoint.new(0.943,0.39,0),NumberSequenceKeypoint.new(0.999,0.7,0),NumberSequenceKeypoint.new(1,1,0)}})
	end
end
track(RunService.Heartbeat:Connect(function()
	local A=Config['Local Player Visuals']
	if A.ParticleAura then
		if not auraPart then buildAuraEmitters(A.ParticleAuraValue) end
		local hrp=LocalPlayer.Character and LocalPlayer.Character:FindFirstChild('HumanoidRootPart')
		if auraPart and hrp then
			if A.ParticleAuraValue=='Rain' then auraPart.CFrame=hrp.CFrame+Vector3.new(0,3.5,0)
			elseif A.ParticleAuraValue=='Ritual' then auraPart.CFrame=hrp.CFrame+Vector3.new(0,-2.99,0)
			else auraPart.CFrame=hrp.CFrame end
		end
	elseif auraPart then
		auraPart:Destroy(); auraPart=nil; auraEmitters={}
	end
end))

-- ######################## 力场身体/帽子 (juju 移植) ########################
local limb_colors={Head="HeadColor",UpperTorso="TorsoColor",LowerTorso="TorsoColor",LeftFoot="LeftLegColor",LeftLowerLeg="LeftLegColor",LeftUpperLeg="LeftLegColor",RightFoot="RightLegColor",RightLowerLeg="RightLegColor",RightUpperLeg="RightLegColor",LeftHand="LeftArmColor",LeftLowerArm="LeftArmColor",LeftUpperArm="LeftArmColor",RightHand="RightArmColor",RightLowerArm="RightArmColor",RightUpperArm="RightArmColor"}
local function restoreLimbColor(p,hum)
	pcall(function()
		local hd=hum and hum.HumanoidDescription
		local desc=hd and limb_colors[p.Name] and hd[limb_colors[p.Name]] or nil
		if desc then p.Color=desc end
	end)
end
function applyForcefieldVisuals()
	local L=Config['Local Player Visuals']
	local ch=LocalPlayer.Character if not ch then return end
	local hum=ch:FindFirstChildOfClass('Humanoid')
	for _,p in pairs(ch:GetChildren()) do
		if p:IsA('BasePart') and p.Name~='HumanoidRootPart' and p.Name~='RootJoint' then
			local sz=p.Size
			if sz and sz.X*sz.Y*sz.Z<0.125 then p.Material=Enum.Material.Plastic; p.Transparency=0
			elseif L.ForcefieldBody then
				p.Material=Enum.Material.ForceField; p.Color=L.ForcefieldBodyColor; p.Transparency=L.ForcefieldBodyTransparency
			else
				p.Material=Enum.Material.Plastic; p.Transparency=0; restoreLimbColor(p,hum)
			end
		elseif p:IsA('Accessory') then
			local h=p:FindFirstChildOfClass('MeshPart') or p:FindFirstChildOfClass('Part')
			if h and h.Size.X*h.Size.Y*h.Size.Z>=0.125 then
				if L.ForcefieldHats then
					h.Material=Enum.Material.ForceField; h.Color=L.ForcefieldHatsColor; h.Transparency=L.ForcefieldHatsTransparency
				else
					h.Material=Enum.Material.Plastic; h.Transparency=0
				end
			end
		end
	end
end
function restoreForcefieldVisuals()
	local ch=LocalPlayer.Character if not ch then return end
	local hum=ch:FindFirstChildOfClass('Humanoid')
	for _,p in pairs(ch:GetChildren()) do
		if p:IsA('BasePart') and p.Name~='HumanoidRootPart' then p.Material=Enum.Material.Plastic; p.Transparency=0; restoreLimbColor(p,hum)
		elseif p:IsA('Accessory') then local h=p:FindFirstChildOfClass('MeshPart') or p:FindFirstChildOfClass('Part') if h then h.Material=Enum.Material.Plastic; h.Transparency=0 end end
	end
end
track(LocalPlayer.CharacterAdded:Connect(function() task.wait(1) applyForcefieldVisuals() end))

-- ######################## Hitsounds (free.txt 移植) ########################
local hitsoundList={
["Bubble"]="rbxassetid://6534947588",["Lazer"]="rbxassetid://130791043",["Pick"]="rbxassetid://1347140027",["Pop"]="rbxassetid://198598793",["Rust"]="rbxassetid://1255040462",["Sans"]="rbxassetid://3188795283",["Fart"]="rbxassetid://130833677",["Big"]="rbxassetid://5332005053",["Vine"]="rbxassetid://5332680810",["UwU"]="rbxassetid://8679659744",["Bruh"]="rbxassetid://4578740568",["Skeet"]="rbxassetid://5633695679",["Neverlose"]="rbxassetid://6534948092",["Fatality"]="rbxassetid://6534947869",["Bonk"]="rbxassetid://5766898159",["Minecraft"]="rbxassetid://5869422451",["Gamesense"]="rbxassetid://4817809188",["RIFK7"]="rbxassetid://9102080552",["Bamboo"]="rbxassetid://3769434519",["Crowbar"]="rbxassetid://546410481",["Weeb"]="rbxassetid://6442965016",["Beep"]="rbxassetid://8177256015",["Bambi"]="rbxassetid://8437203821",["Stone"]="rbxassetid://3581383408",["Old Fatality"]="rbxassetid://6607142036",["Click"]="rbxassetid://8053704437",["Ding"]="rbxassetid://7149516994",["Snow"]="rbxassetid://6455527632",["Laser"]="rbxassetid://7837461331",["Mario"]="rbxassetid://2815207981",["Steve"]="rbxassetid://4965083997",["Call of Duty"]="rbxassetid://5952120301",["Bat"]="rbxassetid://3333907347",["TF2 Critical"]="rbxassetid://296102734",["Saber"]="rbxassetid://8415678813",["Baimware"]="rbxassetid://3124331820",["Osu"]="rbxassetid://7149255551",["TF2"]="rbxassetid://2868331684",["Slime"]="rbxassetid://6916371803",["Among Us"]="rbxassetid://5700183626",["One"]="rbxassetid://7380502345"}
track(hitPlayer:Connect(function(pl,char,dmg)
	local H=Config['Hitsounds']
	if not H.Enabled then return end
	local id=hitsoundList[H.Selected] if not id then return end
	pcall(function()
		local s=Instance.new("Sound"); s.SoundId=id; s.Volume=H.Volume; s.Parent=Workspace; s:Play()
		s.Ended:Connect(function() pcall(function() s:Destroy() end) end)
	end)
end))

-- ######################## 新增 UI 段 (粒子光环 / 力场 / Feature Indicators / Hitsounds) ########################
local paBox=CreateSection(Pages.Visuals.L,"ParticleAura")
CreateToggle(paBox,"ParticleAura",function() return Config['Local Player Visuals'].ParticleAura end,function(v) Config['Local Player Visuals'].ParticleAura=v;if v then buildAuraEmitters(Config['Local Player Visuals'].ParticleAuraValue) elseif auraPart then auraPart:Destroy();auraPart=nil;auraEmitters={} end end)
CreateDropdown(paBox,"AuraValue",{"Swirl","Bubble","Air","Ritual","Rain","Skibidi RedRizz","Bolts"},function() return Config['Local Player Visuals'].ParticleAuraValue end,function(v) Config['Local Player Visuals'].ParticleAuraValue=v;if Config['Local Player Visuals'].ParticleAura then buildAuraEmitters(v) end end)
CreateColorPicker(paBox,"AuraColor",function() return Config['Local Player Visuals'].ParticleAuraColor end,function(v) Config['Local Player Visuals'].ParticleAuraColor=v;if Config['Local Player Visuals'].ParticleAura then buildAuraEmitters(Config['Local Player Visuals'].ParticleAuraValue) end end)
local ffBox=CreateSection(Pages.Visuals.L,"Forcefield")
CreateToggle(ffBox,"ForcefieldBody",function() return Config['Local Player Visuals'].ForcefieldBody end,function(v) Config['Local Player Visuals'].ForcefieldBody=v;applyForcefieldVisuals() end)
CreateColorPicker(ffBox,"ForcefieldBodyColor",function() return Config['Local Player Visuals'].ForcefieldBodyColor end,function(v) Config['Local Player Visuals'].ForcefieldBodyColor=v;applyForcefieldVisuals() end)
CreateToggle(ffBox,"ForcefieldHats",function() return Config['Local Player Visuals'].ForcefieldHats end,function(v) Config['Local Player Visuals'].ForcefieldHats=v;applyForcefieldVisuals() end)
CreateColorPicker(ffBox,"ForcefieldHatsColor",function() return Config['Local Player Visuals'].ForcefieldHatsColor end,function(v) Config['Local Player Visuals'].ForcefieldHatsColor=v;applyForcefieldVisuals() end)
local hsBox2=CreateSection(Pages.Aim.R,"Hitsounds (free)")
CreateToggle(hsBox2,"Hitsounds",function() return Config['Hitsounds'].Enabled end,function(v) Config['Hitsounds'].Enabled=v end)
CreateDropdown(hsBox2,"HitsoundSelect",{"Bubble","Lazer","Pick","Pop","Rust","Sans","Fart","Big","Vine","UwU","Bruh","Skeet","Neverlose","Fatality","Bonk","Minecraft","Gamesense","RIFK7","Bamboo","Crowbar","Weeb","Beep","Bambi","Stone","Old Fatality","Click","Ding","Snow","Laser","Mario","Steve","Call of Duty","Bat","TF2 Critical","Saber","Baimware","Osu","TF2","Slime","Among Us","One"},function() return Config['Hitsounds'].Selected end,function(v) Config['Hitsounds'].Selected=v end)
CreateSlider(hsBox2,"HitsoundVolume",1,50,function() return math.floor(Config['Hitsounds'].Volume*10) end,function(v) Config['Hitsounds'].Volume=v/10 end)

-- 新增功能的中文翻译
Translations.CN.Aimbot="瞄准 (juju)";Translations.CN.AutoSelect="自动选目标";Translations.CN.AutoSelectDelay="选择延迟(ms)";Translations.CN.Sticky="粘住目标";Translations.CN.HitPart="命中部位";Translations.CN.Prediction="预判";Translations.CN.MaxDistance="最大距离";Translations.CN.UntargetKnocked="目标被K.O时解除"
Translations.CN.SilentAim="静默自瞄";Translations.CN.SilentHitChance="命中率%";Translations.CN.SilentFOV="自瞄FOV";Translations.CN.SilentFOVSize="自瞄FOV大小";Translations.CN.SilentFOVColor="自瞄FOV颜色";Translations.CN.SilentLine="自瞄线";Translations.CN.SilentLineColor="自瞄线颜色"
Translations.CN.AimAssist="瞄准辅助";Translations.CN.AssistValue="辅助方式";Translations.CN.AssistSmooth="平滑度";Translations.CN.AssistFOV="辅助FOV";Translations.CN.AssistFOVSize="辅助FOV大小";Translations.CN.AssistFOVColor="辅助FOV颜色";
Translations.CN.Triggerbot="自动扳机";Translations.CN.TriggerDelay="扳机延迟(ms)";Translations.CN.TriggerRadius="扳机半径";Translations.CN.TriggerJumpPred="跳跃预测";Translations.CN.TriggerFirstPerson="仅第一人称"
Translations.CN.Hitsounds="击杀音效";Translations.CN.HitsoundSelect="音效选择";Translations.CN.HitsoundVolume="音量"
Translations.CN.Desync="假同步";Translations.CN.DesyncMode="模式";Translations.CN.VelocityDesync="速度假同步";Translations.CN.VelocityMode="速度模式";Translations.CN.MultiplierVal="倍率";Translations.CN.RandomVal="随机值";Translations.CN.NetworkDesync="网络假同步";Translations.CN.NetworkMode="网络模式";Translations.CN.RandomTP="随机传送";Translations.CN.TPHOff="水平偏移";Translations.CN.TPVOff="垂直偏移";Translations.CN.ShowEye="显示实际位置(眼睛)"
Translations.CN.ParticleAura="粒子光环";Translations.CN.AuraValue="光环类型";Translations.CN.AuraColor="光环颜色"
Translations.CN.Forcefield="力场";Translations.CN.ForcefieldBody="力场身体";Translations.CN.ForcefieldBodyColor="身体颜色";Translations.CN.ForcefieldHats="力场帽子";Translations.CN.ForcefieldHatsColor="帽子颜色"
Translations.CN.KDPColor="指示颜色"
Translations.EN.RageDesyncPos="Desync position";Translations.CN.RageDesyncPos="Desync 位置"
Translations.EN.AutoSortNow="Sort now";Translations.CN.AutoSortNow="立即排序"
Translations.EN.AccessoryAdder="Accessory Adder";Translations.CN.AccessoryAdder="饰品添加"
Translations.EN.AutoSlot1="Slot 1 (item name)"
Translations.CN.AutoSlot1="槽位 1 (物品名)"
Translations.EN.AutoSlot2="Slot 2 (item name)"
Translations.CN.AutoSlot2="槽位 2 (物品名)"
Translations.EN.AutoSlot3="Slot 3 (item name)"
Translations.CN.AutoSlot3="槽位 3 (物品名)"
Translations.EN.AutoSlot4="Slot 4 (item name)"
Translations.CN.AutoSlot4="槽位 4 (物品名)"
Translations.EN.AutoSlot5="Slot 5 (item name)"
Translations.CN.AutoSlot5="槽位 5 (物品名)"
Translations.EN.AutoSlot6="Slot 6 (item name)"
Translations.CN.AutoSlot6="槽位 6 (物品名)"
Translations.EN.AutoSlot7="Slot 7 (item name)"
Translations.CN.AutoSlot7="槽位 7 (物品名)"
Translations.EN.AutoSlot8="Slot 8 (item name)"
Translations.CN.AutoSlot8="槽位 8 (物品名)"
Translations.EN.AutoSlot9="Slot 9 (item name)"
Translations.CN.AutoSlot9="槽位 9 (物品名)"
Translations.EN.KDPSize="Indicator Size";Translations.EN.KDPFont="Indicator Font"
Translations.CN.KDPSize="指示大小";Translations.CN.KDPFont="指示字体"
-- ######################## 动画修改器 (free 移植: 14 套动画预设) ########################
local AnimKeepOnDeath=false
local AnimOptions={["Idle1"]="http://www.roblox.com/asset/?id=180435571",["Idle2"]="http://www.roblox.com/asset/?id=180435792",["Walk"]="http://www.roblox.com/asset/?id=180426354",["Run"]="http://www.roblox.com/asset/?id=180426354",["Jump"]="http://www.roblox.com/asset/?id=125750702",["Climb"]="http://www.roblox.com/asset/?id=180436334",["Fall"]="http://www.roblox.com/asset/?id=180436148"}
local AnimSets={
["Default"]={idle1="http://www.roblox.com/asset/?id=180435571",idle2="http://www.roblox.com/asset/?id=180435792",walk="http://www.roblox.com/asset/?id=180426354",run="http://www.roblox.com/asset/?id=180426354",jump="http://www.roblox.com/asset/?id=125750702",climb="http://www.roblox.com/asset/?id=180436334",fall="http://www.roblox.com/asset/?id=180436148"},
["Ninja"]={idle1="http://www.roblox.com/asset/?id=656117400",idle2="http://www.roblox.com/asset/?id=656118341",walk="http://www.roblox.com/asset/?id=656121766",run="http://www.roblox.com/asset/?id=656118852",jump="http://www.roblox.com/asset/?id=656117878",climb="http://www.roblox.com/asset/?id=656114359",fall="http://www.roblox.com/asset/?id=656115606"},
["Superhero"]={idle1="http://www.roblox.com/asset/?id=616111295",idle2="http://www.roblox.com/asset/?id=616113536",walk="http://www.roblox.com/asset/?id=616122287",run="http://www.roblox.com/asset/?id=616117076",jump="http://www.roblox.com/asset/?id=616115533",climb="http://www.roblox.com/asset/?id=616104706",fall="http://www.roblox.com/asset/?id=616108001"},
["Robot"]={idle1="http://www.roblox.com/asset/?id=616088211",idle2="http://www.roblox.com/asset/?id=616089559",walk="http://www.roblox.com/asset/?id=616095330",run="http://www.roblox.com/asset/?id=616091570",jump="http://www.roblox.com/asset/?id=616090535",climb="http://www.roblox.com/asset/?id=616086039",fall="http://www.roblox.com/asset/?id=616087089"},
["Cartoon"]={idle1="http://www.roblox.com/asset/?id=742637544",idle2="http://www.roblox.com/asset/?id=742638445",walk="http://www.roblox.com/asset/?id=742640026",run="http://www.roblox.com/asset/?id=742638842",jump="http://www.roblox.com/asset/?id=742637942",climb="http://www.roblox.com/asset/?id=742636889",fall="http://www.roblox.com/asset/?id=742637151"},
["Catwalk"]={idle1="http://www.roblox.com/asset/?id=133806214992291",idle2="http://www.roblox.com/asset/?id=94970088341563",walk="http://www.roblox.com/asset/?id=109168724482748",run="http://www.roblox.com/asset/?id=81024476153754",jump="http://www.roblox.com/asset/?id=116936326516985",climb="http://www.roblox.com/asset/?id=119377220967554",fall="http://www.roblox.com/asset/?id=92294537340807"},
["Zombie"]={idle1="http://www.roblox.com/asset/?id=616158929",idle2="http://www.roblox.com/asset/?id=616160636",walk="http://www.roblox.com/asset/?id=616168032",run="http://www.roblox.com/asset/?id=616163682",jump="http://www.roblox.com/asset/?id=616161997",climb="http://www.roblox.com/asset/?id=616156119",fall="http://www.roblox.com/asset/?id=616157476"},
["Mage"]={idle1="http://www.roblox.com/asset/?id=707742142",idle2="http://www.roblox.com/asset/?id=707855907",walk="http://www.roblox.com/asset/?id=707897309",run="http://www.roblox.com/asset/?id=707861613",jump="http://www.roblox.com/asset/?id=707853694",climb="http://www.roblox.com/asset/?id=707826056",fall="http://www.roblox.com/asset/?id=707829716"},
["Pirate"]={idle1="http://www.roblox.com/asset/?id=750785693",idle2="http://www.roblox.com/asset/?id=750782770",walk="http://www.roblox.com/asset/?id=750785693",run="http://www.roblox.com/asset/?id=750782770",jump="http://www.roblox.com/asset/?id=750782770",climb="http://www.roblox.com/asset/?id=750782770",fall="http://www.roblox.com/asset/?id=750782770"},
["Knight"]={idle1="http://www.roblox.com/asset/?id=657595757",idle2="http://www.roblox.com/asset/?id=657568135",walk="http://www.roblox.com/asset/?id=657552124",run="http://www.roblox.com/asset/?id=657564596",jump="http://www.roblox.com/asset/?id=657560148",climb="http://www.roblox.com/asset/?id=657556206",fall="http://www.roblox.com/asset/?id=657552124"},
["Vampire"]={idle1="http://www.roblox.com/asset/?id=1083465857",idle2="http://www.roblox.com/asset/?id=1083465857",walk="http://www.roblox.com/asset/?id=1083465857",run="http://www.roblox.com/asset/?id=1083465857",jump="http://www.roblox.com/asset/?id=1083465857",climb="http://www.roblox.com/asset/?id=1083465857",fall="http://www.roblox.com/asset/?id=1083465857"},
["Bubbly"]={idle1="http://www.roblox.com/asset/?id=910004836",idle2="http://www.roblox.com/asset/?id=910009958",walk="http://www.roblox.com/asset/?id=910034870",run="http://www.roblox.com/asset/?id=910025107",jump="http://www.roblox.com/asset/?id=910016857",climb="http://www.roblox.com/asset/?id=910009958",fall="http://www.roblox.com/asset/?id=910009958"},
["Elder"]={idle1="http://www.roblox.com/asset/?id=845386501",idle2="http://www.roblox.com/asset/?id=845397899",walk="http://www.roblox.com/asset/?id=845403856",run="http://www.roblox.com/asset/?id=845386501",jump="http://www.roblox.com/asset/?id=845386501",climb="http://www.roblox.com/asset/?id=845386501",fall="http://www.roblox.com/asset/?id=845386501"},
["Toy"]={idle1="http://www.roblox.com/asset/?id=782841498",idle2="http://www.roblox.com/asset/?id=782841498",walk="http://www.roblox.com/asset/?id=782841498",run="http://www.roblox.com/asset/?id=782841498",jump="http://www.roblox.com/asset/?id=782841498",climb="http://www.roblox.com/asset/?id=782841498",fall="http://www.roblox.com/asset/?id=782841498"}
}
local AnimNames={"Default","Ninja","Superhero","Robot","Cartoon","Catwalk","Zombie","Mage","Pirate","Knight","Vampire","Bubbly","Elder","Toy"}
function applyCustomAnimations(character)
	if not character then return end
	local Animate=character:FindFirstChild("Animate")
	if not Animate then return end
	local ClonedAnimate=Animate:Clone()
	ClonedAnimate.idle.Animation1.AnimationId=AnimOptions["Idle1"]
	ClonedAnimate.idle.Animation2.AnimationId=AnimOptions["Idle2"]
	ClonedAnimate.walk.WalkAnim.AnimationId=AnimOptions["Walk"]
	ClonedAnimate.run.RunAnim.AnimationId=AnimOptions["Run"]
	ClonedAnimate.jump.JumpAnim.AnimationId=AnimOptions["Jump"]
	ClonedAnimate.climb.ClimbAnim.AnimationId=AnimOptions["Climb"]
	ClonedAnimate.fall.FallAnim.AnimationId=AnimOptions["Fall"]
	Animate:Destroy()
	ClonedAnimate.Parent=character
end
track(LocalPlayer.CharacterAdded:Connect(function(character)
	if AnimKeepOnDeath then task.wait(1) applyCustomAnimations(character) end
end))

-- ######################## God Block 自动格挡 (free 移植) ########################
local godBlockConn=nil
local BlockedAnimations={"rbxassetid://2788289281","rbxassetid://507766388","rbxassetid://2788292075","rbxassetid://278829075","rbxassetid://4798175381","rbxassetid://2953512033","rbxassetid://2788309982","rbxassetid://2788312709","rbxassetid://2788313790","rbxassetid://2788316350","rbxassetid://2788315673","rbxassetid://2788314837"}
pcall(function() ReplicatedStorage:WaitForChild("ClientAnimations").Block.AnimationId="rbxassetid://0" end)
function startGodBlock()
	if godBlockConn then godBlockConn:Disconnect() godBlockConn=nil end
	godBlockConn=RunService.Stepped:Connect(function()
		if not Config['God Block'].Enabled then return end
		local ch=LocalPlayer.Character
		if ch and ch:FindFirstChild(GameCfg.folderName) then
			local be=ch:FindFirstChild(GameCfg.folderName)
			if be:FindFirstChild('Block') then be:FindFirstChild('Block'):Destroy() end
			local tool=ch:FindFirstChildWhichIsA('Tool')
			local mev=getMainEvent()
			if tool and getToolAmmo(tool) then
				if mev then pcall(function() mev:FireServer('Block', false) end) end
			else
				if mev then pcall(function() mev:FireServer('Block', true) end) end
				task.wait()
				if mev then pcall(function() mev:FireServer('Block', false) end) end
			end
		end
	end)
end
function startHideBlockAnims()
	RunService:BindToRenderStep('Hide - Block', 0, function()
		if not Config['God Block'].HideAnimations then return end
		local ch=LocalPlayer.Character
		if ch then
			local hum=ch:FindFirstChildWhichIsA('Humanoid')
			if hum then
				for _,tr in pairs(hum:GetPlayingAnimationTracks()) do
					if table.find(BlockedAnimations, tr.Animation and tr.Animation.AnimationId) then pcall(function() tr:Stop() end) end
				end
			end
		end
	end)
end

-- ######################## Kill Say (free 移植, 可自定义内容) ########################
track(hitPlayer:Connect(function(player, char, damage)
	local KS=Config['Kill Say']
	if not (KS.Enabled and KS.Message and KS.Message~='') then return end
	local hum=char and char:FindFirstChildOfClass('Humanoid')
	if hum and hum.Health<=0 then
		pcall(function() ReplicatedStorage.DefaultChatSystemChatEvents.SayMessageRequest:FireServer(KS.Message, "All") end)
	end
end))

-- ######################## Chat Spy (free 移植) ########################
local chatSpyEnabled=false
local chatSpyReady=false
function setupChatSpy()
	if chatSpyReady then return end
	chatSpyReady=true
	local player=Players.LocalPlayer
	local getmsg=ReplicatedStorage:WaitForChild("DefaultChatSystemChatEvents"):WaitForChild("OnMessageDoneFiltering")
	local function onChatted(p,msg)
		if not chatSpyEnabled then return end
		if p==player then return end
		msg=msg:gsub("[\n\r]",''):gsub("\t",' '):gsub("[ ]+",' ')
		local hidden=true
		local conn=getmsg.OnClientEvent:Connect(function(packet,channel)
			if packet.SpeakerUserId==p.UserId and packet.Message==msg:sub(#msg-#packet.Message+1) and (channel=="All" or (channel=="Team" and Players[packet.FromSpeaker].Team==player.Team)) then hidden=false end
		end)
		task.wait(0.5)
		conn:Disconnect()
		if hidden then
			game:GetService('StarterGui'):SetCore("ChatMakeSystemMessage",{Text="{SPY} ["..p.Name.."]: "..msg,Color=Color3.fromRGB(0,255,255),Font=Enum.Font.SourceSansBold,TextSize=18})
		end
	end
	for _,p in ipairs(Players:GetPlayers()) do p.Chatted:Connect(function(msg) onChatted(p,msg) end) end
	Players.PlayerAdded:Connect(function(p) p.Chatted:Connect(function(msg) onChatted(p,msg) end) end)
end

local kbdBox=CreateSection(Pages.Visuals.L,"KeybindDisplay")
CreateDropdown(kbdBox,"KDPos",{"Left","Right"},function() return Config['Visual Awareness'].KeybindDisplayPos end,function(v) Config['Visual Awareness'].KeybindDisplayPos=v;updateKeybindDisplay() end)
CreateColorPicker(kbdBox,"KDColor",function() return Config['Visual Awareness'].KeybindDisplayColor end,function(v) Config['Visual Awareness'].KeybindDisplayColor=v;updateKeybindDisplay() end)
CreateSlider(kbdBox,"KDSize",8,24,function() return Config['Visual Awareness'].KeybindDisplaySize end,function(v) Config['Visual Awareness'].KeybindDisplaySize=v;updateKeybindDisplay() end)
CreateDropdown(kbdBox,"KDFont",{"Plex","UI","Flex","Monospace"},function() return Config['Visual Awareness'].KeybindDisplayFont end,function(v) Config['Visual Awareness'].KeybindDisplayFont=v;updateKeybindDisplay() end)
CreateLabel(kbdBox,"热键状态指示: 可拖动调整位置")

-- ######################## 新增功能 UI (Chat Spy / God Block / Kill Say / 动画修改器) ########################
local spyBox=CreateSection(Pages.Misc.R,"ChatSpy")
CreateToggle(spyBox,"ChatSpy",function() return chatSpyEnabled end,function(v) chatSpyEnabled=v;if v then setupChatSpy() end end)
CreateLabel(spyBox,"窥屏: 显示别人的隐藏消息")
local gbBox=CreateSection(Pages.Misc.R,"GodBlock")
CreateToggle(gbBox,"GodBlock",function() return Config['God Block'].Enabled end,function(v) Config['God Block'].Enabled=v;if v then startGodBlock() else if godBlockConn then godBlockConn:Disconnect() godBlockConn=nil end end end)
CreateToggle(gbBox,"HideBlockAnims",function() return Config['God Block'].HideAnimations end,function(v) Config['God Block'].HideAnimations=v end)
local ksBox=CreateSection(Pages.Misc.R,"KillSay")
CreateToggle(ksBox,"KillSay",function() return Config['Kill Say'].Enabled end,function(v) Config['Kill Say'].Enabled=v end)
CreateTextBox(ksBox,"KillSayMsg","输入击杀后说的话",function() return Config['Kill Say'].Message end,function(v) Config['Kill Say'].Message=v end)
local animBox=CreateSection(Pages.Misc.R,"Animation")
CreateDropdown(animBox,"Idle1Dropdown",AnimNames,function() return Config['Animations'].Idle1 end,function(v) Config['Animations'].Idle1=v;AnimOptions["Idle1"]=AnimSets[v].idle1;applyCustomAnimations(LocalPlayer.Character) end)
CreateDropdown(animBox,"Idle2Dropdown",AnimNames,function() return Config['Animations'].Idle2 end,function(v) Config['Animations'].Idle2=v;AnimOptions["Idle2"]=AnimSets[v].idle2;applyCustomAnimations(LocalPlayer.Character) end)
CreateDropdown(animBox,"WalkDropdown",AnimNames,function() return Config['Animations'].Walk end,function(v) Config['Animations'].Walk=v;AnimOptions["Walk"]=AnimSets[v].walk;applyCustomAnimations(LocalPlayer.Character) end)
CreateDropdown(animBox,"RunDropdown",AnimNames,function() return Config['Animations'].Run end,function(v) Config['Animations'].Run=v;AnimOptions["Run"]=AnimSets[v].run;applyCustomAnimations(LocalPlayer.Character) end)
CreateDropdown(animBox,"JumpDropdown",AnimNames,function() return Config['Animations'].Jump end,function(v) Config['Animations'].Jump=v;AnimOptions["Jump"]=AnimSets[v].jump;applyCustomAnimations(LocalPlayer.Character) end)
CreateDropdown(animBox,"ClimbDropdown",AnimNames,function() return Config['Animations'].Climb end,function(v) Config['Animations'].Climb=v;AnimOptions["Climb"]=AnimSets[v].climb;applyCustomAnimations(LocalPlayer.Character) end)
CreateDropdown(animBox,"FallDropdown",AnimNames,function() return Config['Animations'].Fall end,function(v) Config['Animations'].Fall=v;AnimOptions["Fall"]=AnimSets[v].fall;applyCustomAnimations(LocalPlayer.Character) end)
CreateToggle(animBox,"KeepOnDeath",function() return AnimKeepOnDeath end,function(v) AnimKeepOnDeath=v end)

Translations.CN.ChatSpy="聊天窥屏";Translations.CN.GodBlock="自动格挡(God Block)";Translations.CN.HideBlockAnims="隐藏格挡动画";Translations.CN.KillSay="击杀喊话";Translations.CN.KillSayMsg="喊话内容";Translations.CN.Animation="动画修改器";Translations.CN.Idle1Dropdown="待机1";Translations.CN.Idle2Dropdown="待机2";Translations.CN.WalkDropdown="行走";Translations.CN.RunDropdown="奔跑";Translations.CN.JumpDropdown="跳跃";Translations.CN.ClimbDropdown="攀爬";Translations.CN.FallDropdown="下落";Translations.CN.KeepOnDeath="死亡保留";Translations.CN.CamLock="相机锁定(CamLock)";Translations.CN.CamLockSmooth="平滑度";Translations.CN.CamFOV="锁定FOV";Translations.CN.CamFOVVisible="显示FOV";Translations.CN.CamFOVSize="FOV大小";Translations.CN.CamFOVColor="FOV颜色";Translations.CN.KDPos="位置";Translations.CN.KDSize="大小";Translations.CN.KDFont="字体";Translations.CN.KDColor="颜色";Translations.CN.KeybindDisplay="热键指示器"

function buyAmmo(gunName)
	local nm=cleanName(gunName)
	local obj=shopNames[nm.."ammo"]
	if not obj then return end
	local hrp=LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
	if not hrp then return end
	local oldPosition=hrp.CFrame
	local currentTool=LocalPlayer.Character:FindFirstChildOfClass("Tool")
	if currentTool then currentTool.Parent=LocalPlayer.Backpack end
	pcall(function() obj.detector.MaxActivationDistance=math.huge; obj.detector.RequiresLineOfSight=false end)
	hrp.CFrame=obj.button.CFrame-Vector3.new(0,8.8,0)
	task.wait(0.15)
	for i=1,6 do pcall(function() fireclickdetector(obj.detector) end) task.wait(0.06) end
	task.wait(0.2)
	if currentTool then currentTool.Parent=LocalPlayer.Character end
	hrp.CFrame=oldPosition
end


-- ######################## 左上角开关提示 (英文, 避免问号) ########################
toggleStatus=nil
toggleStatusBorn=0
function notifyToggle(name, on)
	if not toggleStatus then
		toggleStatus=Drawing.new("Text");toggleStatus.Size=14;toggleStatus.Font=2;toggleStatus.Outline=true;toggleStatus.OutlineColor=Color3.new(0,0,0);toggleStatus.Visible=false
	end
	toggleStatus.Text=name..(on and " ON" or " OFF")
	toggleStatus.Color=on and Color3.fromRGB(124,110,255) or Color3.fromRGB(150,150,165)
	toggleStatus.Position=Vector2.new(15,40)
	toggleStatus.Visible=true
	toggleStatusBorn=tick()
end
track(RunService.RenderStepped:Connect(function()
	if toggleStatus and toggleStatus.Visible and tick()-toggleStatusBorn>2 then toggleStatus.Visible=false end
end))

print("==========================================")
print("  hate.CC loaded")
local _uiKey=(Config.Keybinds['UI Toggle'] and Config.Keybinds['UI Toggle'].Key)
print("  UI Open Key: "..((_uiKey~=nil and _uiKey~='' and _uiKey) or "Unbound"))
print("  F9 = Panic Hide")
print("==========================================")
