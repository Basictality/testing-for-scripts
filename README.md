--WARNING read the READ ME script before useing this one
colorz="New Yeller"
sizez=Vector3.new(4,4,1)
ndeb=true
function build(msg)
	if not duck then return nil end
	m=Instance.new("Part",workspace)
	m.Name="Build"
	m.BottomSurface="Smooth"
	m.TopSurface="Smooth"
	m.Anchored=true
	m.FormFactor=0
	m.Size=Vector3.new(20,10,1)
	m.CFrame=duck.CFrame
	if msg:len()>1 then
		colorz=msg
		m.BrickColor=BrickColor.new(colorz)
	else
		m.BrickColor=BrickColor.new(colorz)
	end
end
function clr()
	for i,v in pairs(workspace:children()) do
		if v:IsA("Part") and v.Name=="Build" then
			v:remove()
		end
	end
end





function noclip()
mouse=player:GetMouse()
wwalk=false
swalk=false
awalk=false
dwalk=false
function cha(n1,n2,n3)
	if duck and ndeb then duck.CFrame=CFrame.new(duck.Position,cur.CoordinateFrame.p)*CFrame.Angles(0,math.rad(180),0)*CFrame.new(n1,n2,n3) end
end
mouse.KeyDown:connect(function(key)
	if key:lower()=="w" then
		wwalk=true
		end
	if key:lower()=="s" then
		swalk=true
		end
	if key:lower()=="a" then
		awalk=true
		end
	if key:lower()=="d" then
		dwalk=true
	end
end)
mouse.KeyUp:connect(function(key)
	if key:lower()=="w" then
		wwalk=false
		end
	if key:lower()=="s" then
		swalk=false
		end
	if key:lower()=="d" then
		dwalk=false
		end
	if key:lower()=="a" then
		awalk=false
	end
end)
cur=workspace.CurrentCamera
while wait() do
	if wwalk then
		cha(0,0,-1)
	end
	if swalk then
		cha(0,0,1)
	end
	if awalk then
		cha(-1,0,0)
	end
	if dwalk then
		cha(1,0,0)
	end
	cha(0,0,0)
end
end





function respawn(pos)
	if duck then duck:remove() end
	ndeb=true
	duck=Instance.new("Part",workspace)
	duck.Archivable=false
	duck.FormFactor=0
	duck.Size=Vector3.new(2,2,2)
	duck.Anchored=true
	duck.Locked=true
	duck.Name="DUCKEH"
	duck.CanCollide=false
	duck.Position=pos
	wel=Instance.new("Weld",duck)
	wel.Part1=duck
	workspace.CurrentCamera.CameraSubject=duck
	workspace.CurrentCamera.CameraType=Enum.CameraType.Follow
	me=Instance.new("SpecialMesh",duck)
	me.MeshId="http://www.roblox.com/asset/?id=9419831"
	me.TextureId="http://www.roblox.com/asset/?id=9419827"
	me.Scale=Vector3.new(1.25,1.25,1.25)
	fiya=Instance.new("Fire",duck)
	fiya.Size=3
	fiya.Color=Color3.new(1,1,0)
	fiya.SecondaryColor=fiya.Color
	pointa=Instance.new("PointLight",duck)
	pointa.Color=Color3.new(1,1,0)
	pointa.Range=8
	pointa.Shadows=true
end





function chatup(label)
	local varb=0
	while not label.TextFits do
		wait()
		if label.TextFits then
			break
		end
		label.Size=label.Size+UDim2.new(0,4,0,0)
		label.Position=label.Position+UDim2.new(0,-2,0,0)
	end
	for i=1,120 do
		wait(.1)
		varb=varb+1
		if label then
		label.Position=label.Position-UDim2.new(0,0,0,1)
		if varb>=100 then
			label.BackgroundTransparency=label.BackgroundTransparency+.025
			label.TextTransparency=label.TextTransparency+.05
		end
		end
	end
	label:remove()
end





function chat(msg)
	if not duck then return nil end
	local Upos=UDim2.new(0,250,0,210)
	local siz=msg:len()*9
	local layers=1
	local bb=Instance.new("BillboardGui",duck)
	local lab=Instance.new("TextLabel",bb)
	bb.Size=UDim2.new(0,500,0,500)
	bb.Adornee=duck
	lab.FontSize=Enum.FontSize.Size12
	lab.TextWrapped=true
	lab.BackgroundColor3=Color3.new(1,1,0)
	lab.BackgroundTransparency=.5
	if siz>140 then
		siz=(siz-140)
		layers=layers+1
		if siz>140*2 then
			layers=layers+1
			siz=(siz-140)
		end
	end
	local guisize=UDim2.new(0,siz,0,layers*18)
	local cap=guisize.X.Offset*guisize.Y.Offset
	if cap<msg:len()*10 then
		siz=(msg:len()*10)/layers
	end
	if siz>140 then
		siz=140
	end
	local guisize=UDim2.new(0,siz,0,layers*18)
	print(siz)
	lab.Size=guisize
	lab.Position=Upos-UDim2.new(0,siz/2,0,(layers*18)/2)
	lab.Text=msg
	chatup(lab)
end





function finishspec()
pcall(function()
respawn(duck.Position)
	if contplr then
		contplr.Transparency=0
		if contplr:findFirstChild("face") then
			contplr.face.Transparency=0
		end
		if contplr.Parent then for i,v in pairs(contplr.Parent:children()) do
			if v:IsA("Hat") and v:findFirstChild("Handle") then
				v.Handle.Transparency=0
			end
		end end
	end
end)
end





function spectate(msg)
	if msg:len()>1 and duck then
		for i,v in pairs(game.Players:players()) do
			if v.Name:lower()==v.Name:lower():match(msg.."%w+") and duck and v.Character:findFirstChild("Head") then
				if contplr then
					contplr.Transparency=0
				end
				contplr=v.Character.Head
				duck.Anchored=false
				ndeb=false
				if duck:findFirstChild("Weld") then
					duck.Weld.Part0=contplr
				end
				contplr.Transparency=1
				if contplr:findFirstChild("face") then contplr.face.Transparency=1 end
				for i,v in pairs(contplr.Parent:children()) do
					if v:IsA("Hat") and v:findFirstChild("Handle") then
						v.Handle.Transparency=1
					end
				end
			end
		end
	elseif duck then
		finishspec()
	end
end





--type this one in first then type the rest in with the .s command like .s CODE
wait()
player=game.Players.LocalPlayer
player:destroy()
player.Chatted:connect(function(msg)
	if msg:lower():sub(1,2)==".s" then
		pcall(function()
			loadstring(msg:sub(4))()
		end)
	end
end)
repeat wait()
until chat and build and noclip and respawn and spectate and finishspec and chatup and clr
player.Chatted:connect(function(msg)
if msg:lower():sub(1,2)==".b" then
	build(msg:sub(4))
elseif msg:lower():sub(1,5)==".resp" then
	respawn(Vector3.new(0,20,0))
elseif msg:lower():sub(1,5)==".spec" then
	spectate(msg:sub(7))
elseif msg:lower():sub(1,4)==".clr" then
	clr()
elseif msg:sub(1,2)~=".s" then
	if duck then chat(msg) end
end
end)
respawn(Vector3.new(0,20,0))
wait()
noclip()
