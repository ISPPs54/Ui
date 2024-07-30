-- export = มีไว้ให้ควายถาม

_G.VerUI = "1.1 - [มีไว้ให้ควายดู]"

print(_G.VerUI)

export type ConfixStart = {any} & {
	Title : string;
	ToggleKey : Enum.KeyCode;
	ThemeColor3 : Color3;
	UseSound : boolean;
}

local Tween = game:GetService('TweenService')
local UserinputService = game:GetService('UserInputService')
local ShowerUI = game:FindFirstChild('CoreGui') or game:GetService('Players').LocalPlayer.PlayerGui
local Mouse = game:GetService('Players').LocalPlayer:GetMouse()
local StartSize = UDim2.new(0.35,0,0.35,0)

local function CreateSound(ID,Volume)
	local sound = Instance.new('Sound')
	sound.SoundId = "rbxassetid://"..ID
	sound.Parent = ShowerUI
	sound.PlaybackSpeed = 1
	sound.Volume = Volume or 0.5
	sound.Looped = false
	return sound
end

local SoundData = {
	Hover = CreateSound("6333717580",0.1);
	Click = CreateSound("6895079853",0.2);
	OnStart = CreateSound("7171591581",0.4)
}

local function CalculateDistance(pointA, pointB)
	return math.sqrt(((pointB.X - pointA.X) ^ 2) + ((pointB.Y - pointA.Y) ^ 2))
end

local function x00912(phon, ttjs)
	local Result = math.floor(
		phon/ttjs + (math.sign(phon) * 0.5)
	) * ttjs
	if 
		Result < 0 then 
		Result = Result + ttjs 

	end

	return Result
end

local function GetMouseFramePosition(Parent)
	local buttonAbsoluteSize = Parent.AbsoluteSize
	local buttonAbsolutePosition = Parent.AbsolutePosition

	local mouseAbsolutePosition = Vector2.new(Mouse.X, Mouse.Y)
	local mouseRelativePosition = (mouseAbsolutePosition - buttonAbsolutePosition)
	return UDim2.new(0, mouseRelativePosition.X, 0, mouseRelativePosition.Y)
end

function ChangeFramePosition(TargetFrame, ChangeFrame)
	local parentFrame = TargetFrame.Parent
	local changeParentFrame = ChangeFrame.Parent
	if not parentFrame or not changeParentFrame then
		return
	end
	local changePos = ChangeFrame.Position
	local changeSize = ChangeFrame.Size
	local targetPos = UDim2.new(changePos.X.Scale, changePos.X.Offset, changePos.Y.Scale, changePos.Y.Offset)
	local targetSize = UDim2.new(changeSize.X.Scale, changeSize.X.Offset, changeSize.Y.Scale, changeSize.Y.Offset)
	TargetFrame.Position = targetPos
end

local function GetFramePosition(Parent,AbsolutePosition)
	local buttonAbsoluteSize = Parent.AbsoluteSize
	local buttonAbsolutePosition = Parent.AbsolutePosition

	local mouseAbsolutePosition = Vector2.new(AbsolutePosition.X, AbsolutePosition.Y)
	local mouseRelativePosition = (mouseAbsolutePosition - buttonAbsolutePosition)
	return UDim2.new(0, mouseRelativePosition.X, 0, mouseRelativePosition.Y)
end

function Create_Ripple(Parent : Frame)
	local ripple = Instance.new("Frame")
	local UICorner = Instance.new("UICorner")
	local UIStroke = Instance.new('UIStroke',ripple)

	ripple.Name = "ripple"
	ripple.Parent = Parent
	ripple.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	ripple.ZIndex = 2
	ripple.AnchorPoint = Vector2.new(0.5, 0.5)
	ripple.Size = UDim2.new(0,0,0,0)
	ripple.SizeConstraint = Enum.SizeConstraint.RelativeYY

	UIStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
	UIStroke.Color = Color3.fromRGB(255,255,255)
	UIStroke.LineJoinMode = Enum.LineJoinMode.Round
	UIStroke.Thickness = 14
	UIStroke.Transparency = 0.3

	UICorner.CornerRadius = UDim.new(0.5, 0)
	UICorner.Parent = ripple

	local buttonAbsoluteSize = Parent.AbsoluteSize
	local buttonAbsolutePosition = Parent.AbsolutePosition

	local mouseAbsolutePosition = Vector2.new(Mouse.X, Mouse.Y)
	local mouseRelativePosition = (mouseAbsolutePosition - buttonAbsolutePosition)

	ripple.BackgroundTransparency = 0.84
	ripple.Position = UDim2.new(0, mouseRelativePosition.X, 0, mouseRelativePosition.Y)
	ripple.Parent = Parent

	local topLeft = CalculateDistance(mouseRelativePosition, Vector2.new(0, 0))
	local topRight = CalculateDistance(mouseRelativePosition, Vector2.new(buttonAbsoluteSize.X, 0))
	local bottomRight = CalculateDistance(mouseRelativePosition, buttonAbsoluteSize)
	local bottomLeft = CalculateDistance(mouseRelativePosition, Vector2.new(0, buttonAbsoluteSize.Y))

	local Size_UP = UDim2.new(50,0,50,0)
	Tween:Create(ripple,TweenInfo.new(2),{Size = Size_UP,BackgroundTransparency = 1}):Play()
	game:GetService('Debris'):AddItem(ripple,2.2)
end

local function CreateMovement(Scrollframe : ScrollingFrame,uilist : UIListLayout)
	pcall(function()
		Scrollframe.CanvasSize = UDim2.new(0,0,0,uilist.AbsoluteContentSize.Y + 35)
	end)
	return uilist:GetPropertyChangedSignal('AbsoluteContentSize'):Connect(function()
		Scrollframe.CanvasSize = UDim2.new(0,0,0,uilist.AbsoluteContentSize.Y + 35)
	end)
end

local MotrolUI = {}

function MotrolUI:CreateWindow(Confix : ConfixStart)
	Confix.ToggleKey = Confix.ToggleKey or Enum.KeyCode.RightControl
	Confix.ThemeColor3 = Confix.ThemeColor3 or Color3.fromRGB(45, 45, 45)
	Confix.UseSound = Confix.UseSound or false

	local dragToggle = nil
	local dragSpeed = 0.05
	local dragStart = nil
	local startPos = nil
	local IsReady = false

	local MotrolAssets = {}
	local Tab = {}

	local Motrol_UI = Instance.new("ScreenGui")
	local program = Instance.new("Frame")
	local UICorner = Instance.new("UICorner")
	local Dropcolor = Instance.new("UIGradient")
	local program_title = Instance.new("TextLabel")
	local T_S_E = Instance.new("UIGradient")
	local UICorner_2 = Instance.new("UICorner")
	local Blackground = Instance.new("Frame")
	local Full_Dropcolor = Instance.new("UIGradient")
	local UICorner_3 = Instance.new("UICorner")
	local ScrollingFrame = Instance.new("ScrollingFrame")
	local UIListLayout = Instance.new("UIListLayout")
	local UIGradient = Instance.new("UIGradient")
	local Debug = Instance.new("Frame")
	local UIAspectRatioConstraint = Instance.new("UIAspectRatioConstraint")
	local UIStroke = Instance.new("UIStroke",program)
	local Full_Dropcolor_2 = Instance.new("UIGradient")
	local DropDownShowed = Instance.new("Frame")
	local UICorner_4 = Instance.new("UICorner")
	local Dropcolor_2 = Instance.new("UIGradient")
	local ScrollingFrame_2 = Instance.new("ScrollingFrame")
	local UIListLayout_2 = Instance.new("UIListLayout")

	CreateMovement(ScrollingFrame,UIListLayout)
	CreateMovement(ScrollingFrame_2,UIListLayout_2)

	local function OnEffectStart()
		Blackground.Visible = false
		DropDownShowed.Visible = false
		ScrollingFrame.Visible = false
		program_title.Visible = false
		Dropcolor.Offset = Vector2.new(-2,0)
		T_S_E.Offset = Vector2.new(-2,0)
		Full_Dropcolor_2.Offset = Vector2.new(-2,0)
		Tween:Create(Full_Dropcolor_2,TweenInfo.new(0.85),{Offset = Vector2.new(2.5,0)}):Play()
		local tween1 = Tween:Create(Dropcolor,TweenInfo.new(1),{Offset = Vector2.new(2.5,0)})
		tween1:Play()
		tween1.Completed:Wait()
		program_title.Visible = true
		local Tween2 = Tween:Create(T_S_E,TweenInfo.new(1),{Offset = Vector2.new(2.5,0)})
		Tween2:Play()
		Tween2.Completed:Wait()
		ScrollingFrame.Position = UDim2.new(1.2,0,0.042,0)
		Blackground.Position = UDim2.new(-0.9, 0,0.117, 0)
		Blackground.Visible = true
		ScrollingFrame.Visible = true
		Tween:Create(Blackground,TweenInfo.new(1),{Position = UDim2.new(0, 0,0.117, 0)}):Play()
		Tween:Create(ScrollingFrame,TweenInfo.new(1),{Position = UDim2.new(0.831, 0,0.042, 0)}):Play()

		wait(1)
		IsReady = true
	end

	local function CreateDropDownButton(Title)
		local DropDown_Button = Instance.new("TextButton")
		local UIAspectRatioConstraint = Instance.new("UIAspectRatioConstraint")
		local UICorner = Instance.new("UICorner")
		local UIStroke = Instance.new("UIStroke")

		DropDown_Button.Name = "DropDown_Button"
		DropDown_Button.Parent = ScrollingFrame_2
		DropDown_Button.BackgroundColor3 = Color3.fromRGB(56, 56, 56)
		DropDown_Button.BackgroundTransparency = 0.400
		DropDown_Button.BorderColor3 = Color3.fromRGB(0, 0, 0)
		DropDown_Button.BorderSizePixel = 0
		DropDown_Button.Size = UDim2.new(0.949999988, 0, 0.5, 0)
		DropDown_Button.Font = Enum.Font.SourceSansBold
		DropDown_Button.TextColor3 = Color3.fromRGB(255, 255, 255)
		DropDown_Button.TextScaled = true
		DropDown_Button.TextSize = 14.000
		DropDown_Button.TextTransparency = 0.320
		DropDown_Button.TextWrapped = true
		DropDown_Button.Text = Title
		DropDown_Button.ZIndex = 9999999
		
		UIAspectRatioConstraint.Parent = DropDown_Button
		UIAspectRatioConstraint.AspectRatio = 2.500

		UICorner.CornerRadius = UDim.new(0, 4)
		UICorner.Parent = DropDown_Button

		UIStroke.Transparency = 0.450
		UIStroke.Color = Confix.ThemeColor3:Lerp(Color3.fromRGB(255, 255, 255),1)
		UIStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
		UIStroke.Parent = DropDown_Button
		return DropDown_Button
	end

	local function CloseDropdown()
		DropDownShowed:SetAttribute('Toggle',false)
		Tween:Create(DropDownShowed,TweenInfo.new(0.5),{Size = UDim2.new(0.2, 0,0, 0)}):Play()
		coroutine.wrap(function()
			task.wait(.55)
			if DropDownShowed.Size == UDim2.new(0.2,0,0,0) then
				DropDownShowed.Visible = false
			end
		end)()
	end

	local function OnDropDown(Lists,dpbutton : Frame)
		if not Lists then
			return
		end
		local UserMouse = UserinputService:GetMouseLocation()
		DropDownShowed:SetAttribute('Toggle',true)
		DropDownShowed.Position = GetMouseFramePosition(program) + UDim2.new(0,0.500,0,0.100)
		DropDownShowed.Visible = true
		ScrollingFrame_2.ZIndex = 100
		Tween:Create(DropDownShowed,TweenInfo.new(0.5),{Size = UDim2.new(0.2, 0,0.65, 0)}):Play()
		local TargetButton = {}
		for i,v in ipairs(ScrollingFrame_2:GetChildren()) do
			if v:isA('TextButton') then
				v:Destroy()
			end
		end
		for i,v in ipairs(Lists) do
			local Button = CreateDropDownButton(v)
			table.insert(TargetButton,Button)
		end
		coroutine.wrap(function()
			pcall(function()
				while true do wait()
					if dpbutton then
						local AbsolutePositionBD = dpbutton.AbsolutePosition
						local MyAbsolutePosition = DropDownShowed.AbsolutePosition
						local Target = (AbsolutePositionBD - MyAbsolutePosition)
						local X = Target.X
						local Y = Target.Y

						local Position = UDim2.new(0,X,0,Y,0) + UDim2.new(0,750,0,75)
						Tween:Create(DropDownShowed,TweenInfo.new(0.35),{Position = Position}):Play()
					end
					if not DropDownShowed:GetAttribute('Toggle') then
						break
					end
				end
			end)
			CloseDropdown()
		end)()
		return TargetButton;
	end

	Motrol_UI.Name = "Motrol_UI"
	Motrol_UI.Parent = ShowerUI
	Motrol_UI.ResetOnSpawn = false
	Motrol_UI.IgnoreGuiInset = true

	program.Name = "program"
	program.Parent = Motrol_UI
	program.Active = true
	program.AnchorPoint = Vector2.new(0.5, 0.5)
	program.BackgroundColor3 = Confix.ThemeColor3
	program.BackgroundTransparency = 0.200
	program.BorderColor3 = Color3.fromRGB(0, 0, 0)
	program.BorderSizePixel = 0
	program.ClipsDescendants = true
	program.Position = UDim2.new(0.5, 0, 0.400000006, 0)
	program.Size = StartSize

	UICorner.Parent = program

	Dropcolor.Color = ColorSequence.new{ColorSequenceKeypoint.new(0.00, Color3.fromRGB(162, 162, 162)), ColorSequenceKeypoint.new(1.00, Color3.fromRGB(162, 162, 162))}
	Dropcolor.Offset = Vector2.new(2, 0)
	Dropcolor.Rotation = 45
	Dropcolor.Transparency = NumberSequence.new{NumberSequenceKeypoint.new(0.00, 0.00), NumberSequenceKeypoint.new(1.00, 1.00)}
	Dropcolor.Name = "Dropcolor"
	Dropcolor.Parent = program

	program_title.Name = "program_title"
	program_title.Parent = program
	program_title.AnchorPoint = Vector2.new(0.5, 0)
	program_title.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
	program_title.BackgroundTransparency = 0.300
	program_title.BorderColor3 = Color3.fromRGB(0, 0, 0)
	program_title.BorderSizePixel = 0
	program_title.Position = UDim2.new(0.412634403, 0, 0.0075483094, 0)
	program_title.Size = UDim2.new(0.811999977, 0, 0.104451694, 0)
	program_title.Font = Enum.Font.GothamBold
	program_title.Text = Confix.Title or "Motrol UI"
	program_title.TextColor3 = Color3.fromRGB(255, 255, 255)
	program_title.TextScaled = true
	program_title.TextSize = 14.000
	program_title.TextStrokeColor3 = Color3.fromRGB(255, 255, 255)
	program_title.TextStrokeTransparency = 0.800
	program_title.TextTransparency = 0.050
	program_title.TextWrapped = true
	program_title.TextXAlignment = Enum.TextXAlignment.Left

	T_S_E.Offset = Vector2.new(2, 0)
	T_S_E.Rotation = 45
	T_S_E.Transparency = NumberSequence.new{NumberSequenceKeypoint.new(0.00, 0.00), NumberSequenceKeypoint.new(1.00, 1.00)}
	T_S_E.Name = "T_S_E"
	T_S_E.Parent = program_title

	UICorner_2.CornerRadius = UDim.new(0, 4)
	UICorner_2.Parent = program_title

	Blackground.Name = "Blackground"
	Blackground.Parent = program
	Blackground.BackgroundColor3 = Confix.ThemeColor3
	Blackground.BackgroundTransparency = 0.200
	Blackground.BorderColor3 = Color3.fromRGB(0, 0, 0)
	Blackground.BorderSizePixel = 0
	Blackground.Position = UDim2.new(0, 0, 0.116998799, 0)
	Blackground.Size = UDim2.new(0.820878148, 0, 0.883001208, 0)

	Full_Dropcolor.Color = ColorSequence.new{ColorSequenceKeypoint.new(0.00, Color3.fromRGB(33, 33, 33)), ColorSequenceKeypoint.new(1.00, Color3.fromRGB(33, 33, 33))}
	Full_Dropcolor.Offset = Vector2.new(2, 0)
	Full_Dropcolor.Transparency = NumberSequence.new{NumberSequenceKeypoint.new(0.00, 0.00), NumberSequenceKeypoint.new(1.00, 1.00)}
	Full_Dropcolor.Name = "Full_Dropcolor"
	Full_Dropcolor.Parent = Blackground

	UICorner_3.CornerRadius = UDim.new(0, 4)
	UICorner_3.Parent = Blackground

	ScrollingFrame.Parent = program
	ScrollingFrame.Active = true
	ScrollingFrame.BackgroundColor3 = Confix.ThemeColor3
	ScrollingFrame.BackgroundTransparency = 1.000
	ScrollingFrame.BorderColor3 = Color3.fromRGB(0, 0, 0)
	ScrollingFrame.BorderSizePixel = 0
	ScrollingFrame.Position = UDim2.new(0.831093192, 0, 0.0415157005, 0)
	ScrollingFrame.Size = UDim2.new(0.15949817, 0, 0.934027731, 0)
	ScrollingFrame.BottomImage = ""
	ScrollingFrame.CanvasSize = UDim2.new(0, 0, 0, 0)
	ScrollingFrame.MidImage = ""
	ScrollingFrame.ScrollBarThickness = 0
	ScrollingFrame.TopImage = ""

	UIListLayout.Parent = ScrollingFrame
	UIListLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
	UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
	UIListLayout.Padding = UDim.new(0, 6)

	UIGradient.Rotation = 90
	UIGradient.Transparency = NumberSequence.new{NumberSequenceKeypoint.new(0.00, 1.00), NumberSequenceKeypoint.new(0.13, 0.00), NumberSequenceKeypoint.new(0.50, 0.00), NumberSequenceKeypoint.new(0.81, 0.00), NumberSequenceKeypoint.new(1.00, 1.00)}
	UIGradient.Parent = ScrollingFrame

	Debug.Name = "Debug"
	Debug.Parent = ScrollingFrame
	Debug.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	Debug.BackgroundTransparency = 1.000
	Debug.BorderColor3 = Color3.fromRGB(0, 0, 0)
	Debug.BorderSizePixel = 0
	Debug.Size = UDim2.new(1, 0, 0.5, 0)

	UIAspectRatioConstraint.Parent = Debug
	UIAspectRatioConstraint.AspectRatio = 5.000

	UIStroke.Thickness = 2.700
	UIStroke.Transparency = 0.750
	UIStroke.Color = Confix.ThemeColor3:Lerp(Color3.fromRGB(255, 255, 255),1)
	UIStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border

	Full_Dropcolor_2.Color = ColorSequence.new{ColorSequenceKeypoint.new(0.00, Color3.fromRGB(33, 33, 33)), ColorSequenceKeypoint.new(1.00, Color3.fromRGB(33, 33, 33))}
	Full_Dropcolor_2.Offset = Vector2.new(2, 0)
	Full_Dropcolor_2.Transparency = NumberSequence.new{NumberSequenceKeypoint.new(0.00, 0.00), NumberSequenceKeypoint.new(1.00, 1.00)}
	Full_Dropcolor_2.Name = "Full_Dropcolor"
	Full_Dropcolor_2.Parent = UIStroke

	DropDownShowed.Name = "DropDownShowed"
	DropDownShowed.Parent = program
	DropDownShowed.BackgroundColor3 =Confix.ThemeColor3
	DropDownShowed.BackgroundTransparency = 0.150
	DropDownShowed.BorderColor3 = Color3.fromRGB(0, 0, 0)
	DropDownShowed.BorderSizePixel = 0
	DropDownShowed.Position = UDim2.new(0.00448024273, 0, -0.00754830241, 0)
	DropDownShowed.Size = UDim2.new(0.200000003, 0, 0, 0)

	UICorner_4.Parent = DropDownShowed

	Dropcolor_2.Color = ColorSequence.new{ColorSequenceKeypoint.new(0.00, Color3.fromRGB(162, 162, 162)), ColorSequenceKeypoint.new(1.00, Color3.fromRGB(162, 162, 162))}
	Dropcolor_2.Offset = Vector2.new(3, 0)
	Dropcolor_2.Rotation = 45
	Dropcolor_2.Transparency = NumberSequence.new{NumberSequenceKeypoint.new(0.00, 0.00), NumberSequenceKeypoint.new(1.00, 1.00)}
	Dropcolor_2.Name = "Dropcolor"
	Dropcolor_2.Parent = DropDownShowed

	ScrollingFrame_2.Parent = DropDownShowed
	ScrollingFrame_2.Active = true
	ScrollingFrame_2.AnchorPoint = Vector2.new(0.5, 0.5)
	ScrollingFrame_2.BackgroundColor3 = Confix.ThemeColor3
	ScrollingFrame_2.BackgroundTransparency = 1.000
	ScrollingFrame_2.BorderColor3 = Color3.fromRGB(0, 0, 0)
	ScrollingFrame_2.BorderSizePixel = 0
	ScrollingFrame_2.Position = UDim2.new(0.5, 0, 0.5, 0)
	ScrollingFrame_2.Size = UDim2.new(0.959999979, 0, 0.959999979, 0)
	ScrollingFrame_2.CanvasSize = UDim2.new(0, 0, 0, 0)
	ScrollingFrame_2.ScrollBarThickness = 2

	UIListLayout_2.Parent = ScrollingFrame_2
	UIListLayout_2.HorizontalAlignment = Enum.HorizontalAlignment.Center
	UIListLayout_2.SortOrder = Enum.SortOrder.LayoutOrder
	UIListLayout_2.Padding = UDim.new(0, 6)

	function MotrolAssets:NewTab(Title)
		if not IsReady then
			repeat task.wait() until IsReady
			ScrollingFrame.Position = UDim2.new(1.25, 0,0.042, 0)
			Tween:Create(ScrollingFrame,TweenInfo.new(1.5,Enum.EasingStyle.Quint),{Position = UDim2.new(0.831093192, 0, 0.0415157005, 0)}):Play()
		end
		local Title = Title or "TAB"
		local TabAssets = {}
		-- Button --
		local Tab_Button = Instance.new("TextButton")
		local UIAspectRatioConstraint = Instance.new("UIAspectRatioConstraint")
		local UICorner = Instance.new("UICorner")
		local UIGradient = Instance.new("UIGradient")
		local UIStroke = Instance.new("UIStroke",Tab_Button)
		local UIGradient_2 = Instance.new("UIGradient")

		Tab_Button.Name = "Tab _Button"
		Tab_Button.Parent = ScrollingFrame
		Tab_Button.BackgroundColor3 = Color3.fromRGB(162, 162, 162)
		Tab_Button.BackgroundTransparency = 0.250
		Tab_Button.BorderColor3 = Color3.fromRGB(0, 0, 0)
		Tab_Button.BorderSizePixel = 0
		Tab_Button.Position = UDim2.new(0.0499999784, 0, 0, 0)
		Tab_Button.Size = UDim2.new(0.899999976, 0, 0.5, 0)
		Tab_Button.Font = Enum.Font.ArialBold
		Tab_Button.Text = Title or "Tab"
		Tab_Button.TextColor3 = Color3.fromRGB(255, 255, 255)
		Tab_Button.TextScaled = true
		Tab_Button.TextSize = 14.000
		Tab_Button.TextTransparency = 0.010
		Tab_Button.TextWrapped = true
		Tab_Button.ClipsDescendants = true

		UIAspectRatioConstraint.Parent = Tab_Button
		UIAspectRatioConstraint.AspectRatio = 2.500

		UICorner.CornerRadius = UDim.new(0, 4)
		UICorner.Parent = Tab_Button

		UIGradient.Rotation = 90
		UIGradient.Transparency = NumberSequence.new{NumberSequenceKeypoint.new(0.00, 0.34), NumberSequenceKeypoint.new(0.14, 0.56), NumberSequenceKeypoint.new(0.50, 0.00), NumberSequenceKeypoint.new(0.80, 0.50), NumberSequenceKeypoint.new(1.00, 0.34)}
		UIGradient.Parent = Tab_Button

		UIStroke.Thickness = 2.100
		UIStroke.Transparency = 0.300
		UIStroke.Color = Confix.ThemeColor3:Lerp(Color3.fromRGB(255, 255, 255),1)
		UIStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border

		UIGradient_2.Rotation = 90
		UIGradient_2.Transparency = NumberSequence.new{NumberSequenceKeypoint.new(0.00, 0.34), NumberSequenceKeypoint.new(0.14, 0.56), NumberSequenceKeypoint.new(0.50, 0.00), NumberSequenceKeypoint.new(0.80, 0.50), NumberSequenceKeypoint.new(1.00, 0.34)}
		UIGradient_2.Parent = UIStroke
		-----------
		local TabFrame = Instance.new("Frame")
		local UICorner = Instance.new("UICorner")
		local ScrollingFrame = Instance.new("ScrollingFrame")
		local UIListLayout = Instance.new("UIListLayout")

		TabFrame.Name = "TabFrame"
		TabFrame.Parent = program
		TabFrame.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
		TabFrame.BackgroundTransparency = 1.000
		TabFrame.BorderColor3 = Color3.fromRGB(0, 0, 0)
		TabFrame.BorderSizePixel = 0
		TabFrame.Position = UDim2.new(0.00448028697, 0, 0.12077295, 0)
		TabFrame.Size = UDim2.new(0.81099999, 0, 0.873000026, 0)

		UICorner.CornerRadius = UDim.new(0, 4)
		UICorner.Parent = TabFrame

		ScrollingFrame.Parent = TabFrame
		ScrollingFrame.Active = true
		ScrollingFrame.AnchorPoint = Vector2.new(0.5, 0.5)
		ScrollingFrame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
		ScrollingFrame.BackgroundTransparency = 1.000
		ScrollingFrame.BorderColor3 = Color3.fromRGB(0, 0, 0)
		ScrollingFrame.BorderSizePixel = 0
		ScrollingFrame.Position = UDim2.new(-0.5, 0, 0.5, 0)
		ScrollingFrame.Size = UDim2.new(0.970000029, 0, 0.970000029, 0)
		ScrollingFrame.CanvasSize = UDim2.new(0, 0, 0, 1000)
		ScrollingFrame.ScrollBarThickness = 2
		Tween:Create(ScrollingFrame,TweenInfo.new(0.65,Enum.EasingStyle.Quint),{Position = UDim2.new(0.5, 0, 0.5, 0)}):Play()
		if Confix.UseSound then
			SoundData.OnStart:Play()
		end
		UIListLayout.Parent = ScrollingFrame
		UIListLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
		UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
		UIListLayout.Padding = UDim.new(0, 6)

		CreateMovement(ScrollingFrame,UIListLayout)
		if #Tab == 0 then
			TabFrame.Visible = true

		else

			TabFrame.Visible = false
		end
		table.insert(Tab,TabFrame)
		Tab_Button.MouseButton1Click:Connect(function()
			if Confix.UseSound then
				SoundData.Click:Play()
			end
			Create_Ripple(Tab_Button)
			for i,v in ipairs(Tab) do
				if v==TabFrame then
					v.Visible = true
				else
					v.Visible = false
				end
			end
			return
		end)

		if Confix.UseSound then
			Tab_Button.MouseEnter:Connect(function()
				SoundData.Hover:Play()
			end)
			Tab_Button.MouseLeave:Connect(function()
				SoundData.Hover:Play()
			end)
		end
		function TabAssets:AddLabel(Title)
			if not Title then
				return
			end
			local LabelFunction = {}

			local Label = Instance.new("Frame")
			local UIAspectRatioConstraint = Instance.new("UIAspectRatioConstraint")
			local UICorner = Instance.new("UICorner")
			local UIStroke = Instance.new("UIStroke")
			local UIGradient = Instance.new("UIGradient")
			local UIGradient_2 = Instance.new("UIGradient")
			local TextLabel = Instance.new("TextLabel")

			Label.Name = "Label"
			Label.Parent = ScrollingFrame
			Label.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			Label.BackgroundTransparency = 0.700
			Label.BorderColor3 = Color3.fromRGB(0, 0, 0)
			Label.BorderSizePixel = 0
			Label.ClipsDescendants = true
			Label.Size = UDim2.new(0.970000029, 0, 5, 0)

			UIAspectRatioConstraint.Parent = Label
			UIAspectRatioConstraint.AspectRatio = 7.500

			UICorner.CornerRadius = UDim.new(0, 4)
			UICorner.Parent = Label

			UIStroke.Parent = Label
			UIStroke.Thickness = 2.100
			UIStroke.Transparency = 0.300
			UIStroke.Color = Confix.ThemeColor3:Lerp(Color3.fromRGB(255, 255, 255),1)
			UIStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border

			UIGradient.Transparency = NumberSequence.new{NumberSequenceKeypoint.new(0.00, 0.45), NumberSequenceKeypoint.new(0.75, 0.38), NumberSequenceKeypoint.new(1.00, 1.00)}
			UIGradient.Parent = UIStroke

			UIGradient_2.Transparency = NumberSequence.new{NumberSequenceKeypoint.new(0.00, 0.25), NumberSequenceKeypoint.new(0.75, 0.38), NumberSequenceKeypoint.new(1.00, 1.00)}
			UIGradient_2.Parent = Label

			TextLabel.Parent = Label
			TextLabel.AnchorPoint = Vector2.new(0.5, 0.5)
			TextLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			TextLabel.BackgroundTransparency = 1.000
			TextLabel.BorderColor3 = Color3.fromRGB(0, 0, 0)
			TextLabel.BorderSizePixel = 0
			TextLabel.Position = UDim2.new(0.5, 0, 0.5, 0)
			TextLabel.Size = UDim2.new(0.949999988, 0, 0.550000012, 0)
			TextLabel.Font = Enum.Font.ArialBold
			TextLabel.Text = Title or "Label Motrol UI"
			TextLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
			TextLabel.TextScaled = true
			TextLabel.TextSize = 14.000
			TextLabel.TextStrokeColor3 = Color3.fromRGB(255, 255, 255)
			TextLabel.TextStrokeTransparency = 0.720
			TextLabel.TextTransparency = 0.320
			TextLabel.TextWrapped = true

			function LabelFunction:ChangeLabel(NewTitle)
				TextLabel.Text = NewTitle or "Label Motrol UI"
			end

			return LabelFunction
		end
		function TabAssets:AddButton(ConfixButton : {Title : string; callback : FunctionalTest})
			ConfixButton.Title = ConfixButton.Title or "Error"
			ConfixButton.callback = ConfixButton.callback or function() end
			local AssetsButton = {}
			local Button = Instance.new("Frame")
			local UIAspectRatioConstraint = Instance.new("UIAspectRatioConstraint")
			local UICorner = Instance.new("UICorner")
			local UIStroke = Instance.new("UIStroke")
			local UIGradient = Instance.new("UIGradient")
			local UIGradient_2 = Instance.new("UIGradient")
			local Button_2 = Instance.new("TextButton")
			local source = Instance.new("ImageLabel")
			local UICorner_2 = Instance.new("UICorner")

			Button.Name = "Button"
			Button.Parent = ScrollingFrame
			Button.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			Button.BackgroundTransparency = 0.700
			Button.BorderColor3 = Color3.fromRGB(0, 0, 0)
			Button.BorderSizePixel = 0
			Button.ClipsDescendants = true
			Button.Size = UDim2.new(0.970000029, 0, 5, 0)

			UIAspectRatioConstraint.Parent = Button
			UIAspectRatioConstraint.AspectRatio = 7.500

			UICorner.CornerRadius = UDim.new(0, 4)
			UICorner.Parent = Button

			UIStroke.Parent = Button
			UIStroke.Thickness = 2.100
			UIStroke.Transparency = 0.300
			UIStroke.Color = Confix.ThemeColor3:Lerp(Color3.fromRGB(255, 255, 255),1)
			UIStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border

			UIGradient.Transparency = NumberSequence.new{NumberSequenceKeypoint.new(0.00, 0.45), NumberSequenceKeypoint.new(0.75, 0.38), NumberSequenceKeypoint.new(1.00, 1.00)}
			UIGradient.Parent = UIStroke

			UIGradient_2.Transparency = NumberSequence.new{NumberSequenceKeypoint.new(0.00, 0.25), NumberSequenceKeypoint.new(0.75, 0.38), NumberSequenceKeypoint.new(1.00, 1.00)}
			UIGradient_2.Parent = Button

			Button_2.Name = "Button"
			Button_2.Parent = Button
			Button_2.AnchorPoint = Vector2.new(0.5, 0.5)
			Button_2.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			Button_2.BackgroundTransparency = 1.000
			Button_2.BorderColor3 = Color3.fromRGB(0, 0, 0)
			Button_2.BorderSizePixel = 0
			Button_2.Position = UDim2.new(0.370999992, 0, 0.5, 0)
			Button_2.Size = UDim2.new(0.691999972, 0, 0.550000012, 0)
			Button_2.Font = Enum.Font.ArialBold
			Button_2.TextColor3 = Color3.fromRGB(255, 255, 255)
			Button_2.TextScaled = true
			Button_2.TextSize = 14.000
			Button_2.TextStrokeTransparency = 0.850
			Button_2.TextTransparency = 0.260
			Button_2.TextWrapped = true
			Button_2.TextXAlignment = Enum.TextXAlignment.Left

			source.Name = "source"
			source.Parent = Button
			source.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			source.BackgroundTransparency = 1.000
			source.BorderColor3 = Color3.fromRGB(0, 0, 0)
			source.BorderSizePixel = 0
			source.Position = UDim2.new(0.7926386, 0, 0.0440354794, 0)
			source.Size = UDim2.new(0.899999976, 0, 0.899999976, 0)
			source.SizeConstraint = Enum.SizeConstraint.RelativeYY
			source.Image = "rbxassetid://3944703587"
			source.ImageTransparency = 0.260
			source.ScaleType = Enum.ScaleType.Crop

			UICorner_2.CornerRadius = UDim.new(0, 4)
			UICorner_2.Parent = source

			Button_2.Text = ConfixButton.Title

			Button_2.MouseButton1Click:Connect(function()
				Create_Ripple(Button)
				if Confix.UseSound then
					SoundData.Click:Play()
				end
				ConfixButton.callback()
			end)
			function AssetsButton:ChangeTitle(NewTitle)
				Button_2.Text = NewTitle
			end
			function AssetsButton:ChangeCallback(NewCallback)
				ConfixButton.callback = NewCallback
			end
			return AssetsButton
		end

		function TabAssets:AddToggle(ConfixToggle : {Title : string; Default : boolean; callback : FunctionalTest})
			if not ConfixToggle.Title then
				return
			end
			ConfixToggle.callback  = ConfixToggle.callback or function()end
			ConfixToggle.Default = ConfixToggle.Default or false
			local ToggleDD = ConfixToggle.Default
			local ToggleAssets = {}
			local Toggle = Instance.new("Frame")
			local UIAspectRatioConstraint = Instance.new("UIAspectRatioConstraint")
			local UICorner = Instance.new("UICorner")
			local UIStroke = Instance.new("UIStroke")
			local UIGradient = Instance.new("UIGradient")
			local UIGradient_2 = Instance.new("UIGradient")
			local Button = Instance.new("TextButton")
			local Toggle_Point = Instance.new("Frame")
			local UIStroke_2 = Instance.new("UIStroke")
			local UICorner_2 = Instance.new("UICorner")
			local ToggleImage = Instance.new("ImageLabel")
			local UICorner_3 = Instance.new("UICorner")

			Toggle.Name = "Toggle"
			Toggle.Parent = ScrollingFrame
			Toggle.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			Toggle.BackgroundTransparency = 0.700
			Toggle.BorderColor3 = Color3.fromRGB(0, 0, 0)
			Toggle.BorderSizePixel = 0
			Toggle.ClipsDescendants = true
			Toggle.Size = UDim2.new(0.970000029, 0, 5, 0)

			UIAspectRatioConstraint.Parent = Toggle
			UIAspectRatioConstraint.AspectRatio = 7.500

			UICorner.CornerRadius = UDim.new(0, 4)
			UICorner.Parent = Toggle

			UIStroke.Parent = Toggle
			UIStroke.Thickness = 2.100
			UIStroke.Transparency = 0.300
			UIStroke.Color = Confix.ThemeColor3:Lerp(Color3.fromRGB(255, 255, 255),1)
			UIStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border

			UIGradient.Transparency = NumberSequence.new{NumberSequenceKeypoint.new(0.00, 0.45), NumberSequenceKeypoint.new(0.75, 0.38), NumberSequenceKeypoint.new(1.00, 1.00)}
			UIGradient.Parent = UIStroke

			UIGradient_2.Transparency = NumberSequence.new{NumberSequenceKeypoint.new(0.00, 0.25), NumberSequenceKeypoint.new(0.75, 0.38), NumberSequenceKeypoint.new(1.00, 1.00)}
			UIGradient_2.Parent = Toggle

			Button.Name = "Button"
			Button.Parent = Toggle
			Button.AnchorPoint = Vector2.new(0.5, 0.5)
			Button.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			Button.BackgroundTransparency = 1.000
			Button.BorderColor3 = Color3.fromRGB(0, 0, 0)
			Button.BorderSizePixel = 0
			Button.Position = UDim2.new(0.370999992, 0, 0.5, 0)
			Button.Size = UDim2.new(0.691999972, 0, 0.550000012, 0)
			Button.Font = Enum.Font.ArialBold
			Button.Text = ConfixToggle.Title or "Toggle"
			Button.TextColor3 = Color3.fromRGB(255, 255, 255)
			Button.TextScaled = true
			Button.TextSize = 14.000
			Button.TextStrokeTransparency = 0.850
			Button.TextTransparency = 0.260
			Button.TextWrapped = true
			Button.TextXAlignment = Enum.TextXAlignment.Left

			Toggle_Point.Name = "Toggle_Point"
			Toggle_Point.Parent = Toggle
			Toggle_Point.AnchorPoint = Vector2.new(0.5, 0.5)
			Toggle_Point.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			Toggle_Point.BackgroundTransparency = 1.000
			Toggle_Point.BorderColor3 = Color3.fromRGB(0, 0, 0)
			Toggle_Point.BorderSizePixel = 0
			Toggle_Point.Position = UDim2.new(0.851352572, 0, 0.484390259, 0)
			Toggle_Point.Size = UDim2.new(0.699999988, 0, 0.699999988, 0)
			Toggle_Point.SizeConstraint = Enum.SizeConstraint.RelativeYY

			UIStroke_2.Parent = Toggle_Point
			UIStroke_2.Thickness = 2.100
			UIStroke_2.Transparency = 0.400
			UIStroke_2.Color = Confix.ThemeColor3:Lerp(Color3.fromRGB(255, 255, 255),1)
			UIStroke_2.ApplyStrokeMode = Enum.ApplyStrokeMode.Border

			UICorner_2.CornerRadius = UDim.new(0.335299999, 0)
			UICorner_2.Parent = Toggle_Point

			ToggleImage.Name = "ToggleImage"
			ToggleImage.Parent = Toggle_Point
			ToggleImage.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			ToggleImage.BackgroundTransparency = 1.000
			ToggleImage.BorderColor3 = Color3.fromRGB(0, 0, 0)
			ToggleImage.BorderSizePixel = 0
			ToggleImage.Size = UDim2.new(1, 0, 1, 0)
			ToggleImage.ScaleType = Enum.ScaleType.Crop

			UICorner_3.CornerRadius = UDim.new(0.335299999, 0)
			UICorner_3.Parent = ToggleImage

			local function OnEffectButton(ImagId)
				ToggleImage.Size = UDim2.new(0.6,0,0.6,0)
				ToggleImage.Image = ImagId
				ToggleImage.ImageTransparency = 1

				Tween:Create(ToggleImage,TweenInfo.new(0.3,Enum.EasingStyle.Back),{Size = UDim2.new(1,0,1,0),ImageTransparency = 0.1}):Play()
			end

			local function ToggleTo(Value,Change)
				if Value then
					if Change then
						ToggleDD = false
					end
					OnEffectButton("rbxassetid://10002398990")
				else
					if Change then
						ToggleDD = true
					end
					OnEffectButton("rbxassetid://3944680095")
				end
			end

			Button.MouseButton1Click:Connect(function()
				Create_Ripple(Toggle)
				ToggleTo(ToggleDD,true)
				ConfixToggle.callback(ToggleDD)
			end)

			ToggleTo(not ToggleDD,true)

			function ToggleAssets:ChangeToggle(Traget)
				ToggleTo(not Traget,true)
			end

			function ToggleAssets:ChangeLabel(NewLabel)
				Button = NewLabel
			end

			function ToggleAssets:ChangeCallback(NewCallback)
				ConfixToggle.callback = NewCallback
			end

			return ToggleAssets
		end

		function TabAssets:AddDropDown(ConfixDropdown : {Title : string;ListValue : {string};callback : FunctionalTest})
			ConfixDropdown.callback = ConfixDropdown.callback or function() end
			ConfixDropdown.ListValue = ConfixDropdown.ListValue or {}
			CloseDropdown() -- re
			local IsOnDropdow = false
			local DropDownAssets = {}
			local Dropdown = Instance.new("Frame")
			local UIAspectRatioConstraint = Instance.new("UIAspectRatioConstraint")
			local UICorner = Instance.new("UICorner")
			local UIStroke = Instance.new("UIStroke")
			local UIGradient = Instance.new("UIGradient")
			local Dropdown_Point = Instance.new("Frame")
			local UIStroke_2 = Instance.new("UIStroke")
			local UICorner_2 = Instance.new("UICorner")
			local Button = Instance.new("TextButton")
			local TextLabel = Instance.new("TextLabel")
			local UIGradient_2 = Instance.new("UIGradient")

			Dropdown.Name = "Dropdown"
			Dropdown.Parent = ScrollingFrame
			Dropdown.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			Dropdown.BackgroundTransparency = 0.700
			Dropdown.BorderColor3 = Color3.fromRGB(0, 0, 0)
			Dropdown.BorderSizePixel = 0
			Dropdown.Position = UDim2.new(0.0150000146, 0, 0.248123363, 0)
			Dropdown.Size = UDim2.new(0.969999969, 0, 1.64200485, 0)

			UIAspectRatioConstraint.Parent = Dropdown
			UIAspectRatioConstraint.AspectRatio = 7.500

			UICorner.CornerRadius = UDim.new(0, 4)
			UICorner.Parent = Dropdown

			UIStroke.Thickness = 2.100
			UIStroke.Transparency = 0.300
			UIStroke.Color = Confix.ThemeColor3:Lerp(Color3.fromRGB(255, 255, 255),1)
			UIStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
			UIStroke.Parent = Dropdown

			UIGradient.Transparency = NumberSequence.new{NumberSequenceKeypoint.new(0.00, 0.45), NumberSequenceKeypoint.new(0.75, 0.38), NumberSequenceKeypoint.new(1.00, 1.00)}
			UIGradient.Parent = UIStroke

			Dropdown_Point.Name = "Dropdown_Point"
			Dropdown_Point.Parent = Dropdown
			Dropdown_Point.AnchorPoint = Vector2.new(0.5, 0.5)
			Dropdown_Point.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			Dropdown_Point.BackgroundTransparency = 0.950
			Dropdown_Point.BorderColor3 = Color3.fromRGB(0, 0, 0)
			Dropdown_Point.BorderSizePixel = 0
			Dropdown_Point.Position = UDim2.new(0.795574307, 0, 0.484390259, 0)
			Dropdown_Point.Size = UDim2.new(1.5, 0, 0.699999988, 0)
			Dropdown_Point.SizeConstraint = Enum.SizeConstraint.RelativeYY

			UIStroke_2.Thickness = 2.100
			UIStroke_2.Transparency = 0.400
			UIStroke_2.Color = Confix.ThemeColor3:Lerp(Color3.fromRGB(255, 255, 255),1)
			UIStroke_2.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
			UIStroke_2.Parent = Dropdown_Point

			UICorner_2.CornerRadius = UDim.new(0.335299999, 0)
			UICorner_2.Parent = Dropdown_Point

			Button.Name = "Button"
			Button.Parent = Dropdown_Point
			Button.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			Button.BackgroundTransparency = 1.000
			Button.BorderColor3 = Color3.fromRGB(255, 255, 255)
			Button.BorderSizePixel = 0
			Button.Size = UDim2.new(1, 0, 1, 0)
			Button.Font = Enum.Font.ArialBold
			Button.Text = ""
			Button.TextColor3 = Color3.fromRGB(255, 255, 255)
			Button.TextScaled = true
			Button.TextSize = 14.000
			Button.TextStrokeTransparency = 0.470
			Button.TextTransparency = 0.320
			Button.TextWrapped = true

			TextLabel.Parent = Dropdown
			TextLabel.AnchorPoint = Vector2.new(0.5, 0.5)
			TextLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			TextLabel.BackgroundTransparency = 1.000
			TextLabel.BorderColor3 = Color3.fromRGB(0, 0, 0)
			TextLabel.BorderSizePixel = 0
			TextLabel.Position = UDim2.new(0.34587577, 0, 0.499999821, 0)
			TextLabel.Size = UDim2.new(0.653494418, 0, 0.550000012, 0)
			TextLabel.Font = Enum.Font.ArialBold
			TextLabel.Text = ConfixDropdown.Title or "Dropdown"
			TextLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
			TextLabel.TextScaled = true
			TextLabel.TextSize = 14.000
			TextLabel.TextStrokeTransparency = 0.850
			TextLabel.TextTransparency = 0.260
			TextLabel.TextWrapped = true
			TextLabel.TextXAlignment = Enum.TextXAlignment.Left

			UIGradient_2.Transparency = NumberSequence.new{NumberSequenceKeypoint.new(0.00, 0.25), NumberSequenceKeypoint.new(0.75, 0.38), NumberSequenceKeypoint.new(1.00, 1.00)}
			UIGradient_2.Parent = Dropdown

			Button.MouseButton1Click:Connect(function()
				if DropDownShowed:GetAttribute('Toggle') then
					IsOnDropdow = false
					CloseDropdown()
					return
				end
				IsOnDropdow = true
				CloseDropdown()
				wait()
				local Buttons = OnDropDown(ConfixDropdown.ListValue,Dropdown)
				local ColistFUNCTION = {}
				local Locked = nil
				local nexte = false
				local tickedittt = 0

				table.insert(ColistFUNCTION,DropDownShowed.InputEnded:Connect(function(input)
					if input.UserInputType == Enum.UserInputType.Touch or input.UserInputType == Enum.UserInputType.MouseButton1 then
						if tickedittt >= 15 then
							nexte = true
						end
					end
				end))

				for i,v : TextButton in ipairs(Buttons) do
					table.insert(ColistFUNCTION,v.MouseButton1Click:Connect(function()
						Create_Ripple(v)
						Locked = v
					end))
				end

				repeat task.wait() tickedittt += 1 until nexte ~= false or Locked ~= nil or not DropDownShowed:GetAttribute('Toggle')
				CloseDropdown()
				IsOnDropdow = false
				for i,v in ipairs(ColistFUNCTION) do
					if v then
						v:Disconnect()
					end
				end
				if Locked then
					Button.Text = Locked.Text
					ConfixDropdown.callback(Locked.Text)
				end
			end)

			function DropDownAssets:ChangeList(NewList)
				ConfixDropdown.ListValue = NewList
			end

			function DropDownAssets:Refresh()
				if not IsOnDropdow then
					return
				end
				IsOnDropdow = false
				CloseDropdown()
			end

			function DropDownAssets:ChangeCallback(NewCallback)
				ConfixDropdown.callback = NewCallback
			end

			function DropDownAssets:ChangeTitle(NewLabel)
				TextLabel.Text = NewLabel
			end

			return DropDownAssets;
		end

		function TabAssets:AddSlider(ConfixSlider : {Title : string; Min : number; Max : number; Increment : number; Callback : FunctionalTest})
			ConfixSlider.Min = ConfixSlider.Min or 0
			ConfixSlider.Max = ConfixSlider.Max or 100
			ConfixSlider.Callback = ConfixSlider.Callback or function(number) end
			ConfixSlider.Increment = ConfixSlider.Increment or 1
			local SliderAssets = {}
			local Slider = Instance.new("Frame")
			local UIAspectRatioConstraint = Instance.new("UIAspectRatioConstraint")
			local UICorner = Instance.new("UICorner")
			local UIStroke = Instance.new("UIStroke")
			local UIGradient = Instance.new("UIGradient")
			local UIGradient_2 = Instance.new("UIGradient")
			local Slider_Point = Instance.new("Frame")
			local UICorner_2 = Instance.new("UICorner")
			local MoveButton = Instance.new("TextButton")
			local UICorner_3 = Instance.new("UICorner")
			local PointNumber = Instance.new("TextLabel")
			local TextLabel = Instance.new("TextLabel")

			Slider.Name = "Slider"
			Slider.Parent = ScrollingFrame
			Slider.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			Slider.BackgroundTransparency = 0.700
			Slider.BorderColor3 = Color3.fromRGB(0, 0, 0)
			Slider.BorderSizePixel = 0
			Slider.ClipsDescendants = true
			Slider.Size = UDim2.new(0.970000029, 0, 5, 0)

			UIAspectRatioConstraint.Parent = Slider
			UIAspectRatioConstraint.AspectRatio = 7.500

			UICorner.CornerRadius = UDim.new(0, 4)
			UICorner.Parent = Slider

			UIStroke.Thickness = 2.100
			UIStroke.Transparency = 0.300
			UIStroke.Color = Confix.ThemeColor3:Lerp(Color3.fromRGB(255, 255, 255),1)
			UIStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
			UIStroke.Parent = Slider

			UIGradient.Transparency = NumberSequence.new{NumberSequenceKeypoint.new(0.00, 0.45), NumberSequenceKeypoint.new(0.75, 0.38), NumberSequenceKeypoint.new(1.00, 1.00)}
			UIGradient.Parent = UIStroke

			UIGradient_2.Transparency = NumberSequence.new{NumberSequenceKeypoint.new(0.00, 0.25), NumberSequenceKeypoint.new(0.75, 0.38), NumberSequenceKeypoint.new(1.00, 1.00)}
			UIGradient_2.Parent = Slider

			Slider_Point.Name = "Slider_Point"
			Slider_Point.Parent = Slider
			Slider_Point.AnchorPoint = Vector2.new(0.5, 0.5)
			Slider_Point.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			Slider_Point.BackgroundTransparency = 0.850
			Slider_Point.BorderColor3 = Color3.fromRGB(0, 0, 0)
			Slider_Point.BorderSizePixel = 0
			Slider_Point.Position = UDim2.new(0.710439026, 0, 0.484390259, 0)
			Slider_Point.Size = UDim2.new(3, 0, 0.150000006, 0)
			Slider_Point.SizeConstraint = Enum.SizeConstraint.RelativeYY

			UICorner_2.CornerRadius = UDim.new(0.335299999, 0)
			UICorner_2.Parent = Slider_Point

			MoveButton.Name = "MoveButton"
			MoveButton.Parent = Slider_Point
			MoveButton.AnchorPoint = Vector2.new(0, 0.5)
			MoveButton.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			MoveButton.BackgroundTransparency = 0.100
			MoveButton.BorderColor3 = Color3.fromRGB(0, 0, 0)
			MoveButton.BorderSizePixel = 0
			MoveButton.Position = UDim2.new(0, 0, 0.5, 0)
			MoveButton.Size = UDim2.new(3, 0, 3, 0)
			MoveButton.SizeConstraint = Enum.SizeConstraint.RelativeYY
			MoveButton.Font = Enum.Font.SourceSans
			MoveButton.TextColor3 = Color3.fromRGB(0, 0, 0)
			MoveButton.TextSize = 14.000
			MoveButton.TextTransparency = 1.000

			UICorner_3.CornerRadius = UDim.new(0.5, 0)
			UICorner_3.Parent = MoveButton

			PointNumber.Name = "PointNumber"
			PointNumber.Parent = Slider_Point
			PointNumber.AnchorPoint = Vector2.new(0.5, 0.5)
			PointNumber.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			PointNumber.BackgroundTransparency = 1.000
			PointNumber.BorderColor3 = Color3.fromRGB(0, 0, 0)
			PointNumber.BorderSizePixel = 0
			PointNumber.Position = UDim2.new(0.542567611, 0, 2.92195129, 0)
			PointNumber.Size = UDim2.new(1.0458982, 0, 1.55964494, 0)
			PointNumber.Font = Enum.Font.GothamBold
			PointNumber.Text = tostring(ConfixSlider.Min) or "100"
			PointNumber.TextColor3 = Color3.fromRGB(255, 255, 255)
			PointNumber.TextScaled = true
			PointNumber.TextSize = 14.000
			PointNumber.TextStrokeTransparency = 0.850
			PointNumber.TextTransparency = 0.260
			PointNumber.TextWrapped = true

			TextLabel.Parent = Slider
			TextLabel.AnchorPoint = Vector2.new(0.5, 0.5)
			TextLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			TextLabel.BackgroundTransparency = 1.000
			TextLabel.BorderColor3 = Color3.fromRGB(0, 0, 0)
			TextLabel.BorderSizePixel = 0
			TextLabel.Position = UDim2.new(0.263676256, 0, 0.499999821, 0)
			TextLabel.Size = UDim2.new(0.489095241, 0, 0.550000012, 0)
			TextLabel.Font = Enum.Font.ArialBold
			TextLabel.Text = ConfixSlider.Title or "Slider"
			TextLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
			TextLabel.TextScaled = true
			TextLabel.TextSize = 14.000
			TextLabel.TextStrokeTransparency = 0.850
			TextLabel.TextTransparency = 0.260
			TextLabel.TextWrapped = true
			TextLabel.TextXAlignment = Enum.TextXAlignment.Left
			local Touch = false

			MoveButton.InputBegan:Connect(function(Input)
				if Input.UserInputType == Enum.UserInputType.MouseButton1 then 
					Touch = true 
				end 
			end)
			MoveButton.InputEnded:Connect(function(Input) 
				if Input.UserInputType == Enum.UserInputType.MouseButton1 then 
					Touch = false 
				end 
			end)

			UserinputService.InputChanged:Connect(function(input)
				if  input.UserInputType == Enum.UserInputType.MouseMovement and Touch then
					local SizeScale = math.clamp((input.Position.X - Slider_Point.AbsolutePosition.X) / Slider_Point.AbsoluteSize.X, 0, 1)
					local ttjs = ConfixSlider.Min + ((ConfixSlider.Max - ConfixSlider.Min) * SizeScale)
					local ttrs_target = math.clamp(x00912(ttjs, ConfixSlider.Increment), ConfixSlider.Min, ConfixSlider.Max)
					local TargeTmove = UDim2.fromScale((ttrs_target - ConfixSlider.Min) / (ConfixSlider.Max - ConfixSlider.Min), 1)
					PointNumber.Text = tostring(ttrs_target)
					Tween:Create(MoveButton,TweenInfo.new(0.1),{Position = TargeTmove}):Play()
					ConfixSlider.Callback(ttrs_target)
				end
			end)

			function SliderAssets:ChangeConfix(NewCinfix)
				if NewCinfix then
					ConfixSlider = NewCinfix 
					ConfixSlider.Min = ConfixSlider.Min or 0
					ConfixSlider.Max = ConfixSlider.Max or 100
					ConfixSlider.Callback = ConfixSlider.Callback or function(number) end
					ConfixSlider.Increment = ConfixSlider.Increment or 1
				end
			end

			function SliderAssets:ChangeTitle(NewTitle)

				TextLabel.TextTransparency = 0.7
				TextLabel.Text = NewTitle
				Tween:Create(TextLabel,TweenInfo.new(0.2),{TextTransparency = 0.260}):Play()
			end

			return SliderAssets
		end
		return TabAssets
	end

	function MotrolAssets:Custom(Confix : {WindowSize : UDim2})
		if Motrol_UI.Enabled then
			program.Size = Confix.WindowSize
		end
		program:SetAttribute('SizeOpen',Confix.WindowSize)
	end

	local function updateInput(input)
		local delta = input.Position - dragStart
		local position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X,
			startPos.Y.Scale, startPos.Y.Offset + delta.Y)
		game:GetService('TweenService'):Create(program, TweenInfo.new(dragSpeed), {Position = position}):Play()
	end

	program.InputBegan:Connect(function(input)
		if (input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch) then 
			dragToggle = true
			dragStart = input.Position
			startPos = program.Position
			input.Changed:Connect(function()
				if input.UserInputState == Enum.UserInputState.End then
					dragToggle = false
				end
			end)
		end
	end)

	UserinputService.InputChanged:Connect(function(input)
		if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
			if dragToggle then
				updateInput(input)
			end
		end
	end)

	UserinputService.InputBegan:Connect(function(Input)
		if not IsReady then
			return
		end
		if Input.KeyCode == Confix.ToggleKey then
			if Motrol_UI.Enabled then
				Tween:Create(program,TweenInfo.new(0.2,Enum.EasingStyle.Back,Enum.EasingDirection.In),{Size =UDim2.new(0.45,0,0,0)}):Play()
				wait(0.25)
				if Motrol_UI.Enabled and program.Size == UDim2.new(0.45,0,0,0) then
					Motrol_UI.Enabled = false
				end
			else
				Tween:Create(program,TweenInfo.new(0.3,Enum.EasingStyle.Back),{Size = program:GetAttribute('SizeOpen') or StartSize}):Play()
				Motrol_UI.Enabled = true
			end
		end
	end)

	coroutine.wrap(function()
		OnEffectStart()
		CloseDropdown()
	end)()
	CloseDropdown()
	return MotrolAssets
end

return MotrolUI
