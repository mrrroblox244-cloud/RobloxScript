# ROBLOX Script

1. **Kill Block (Dødskloss / แผ่นอันตราย)**


```lua
local killBlock = script.Parent

killBlock.Touched:Connect(function(otherPart)
	local character = otherPart.Parent
	local humanoid = character:FindFirstChildOfClass("Humanoid")
	if humanoid then
		humanoid.Health = 0
	end
end)
```


2. **Disappearing Block (Forsvinnende kloss / แผ่นหายตัว)**

```lua
local part = script.Parent
local isTouched = false

part.Touched:Connect(function()
	if not isTouched then
		isTouched = true
		task.wait(0.3)
		part.Transparency = 0.8
		part.CanCollide = false
		task.wait(2)
		part.Transparency = 0
		part.CanCollide = true
		isTouched = false
	end
end)
```

3. **Speed Boost (Fartsokning / แผ่นเพิ่มความเร็ว)**

```lua
local speedPad = script.Parent

speedPad.Touched:Connect(function(otherPart)
	local character = otherPart.Parent
	local humanoid = character:FindFirstChildOfClass("Humanoid")
	if humanoid and humanoid.WalkSpeed == 16 then
		humanoid.WalkSpeed = 40
		task.wait(3)
		humanoid.WalkSpeed = 16
	end
end)
```

4. **High Jump Pad (Hoppepute / แผ่นเด้งสูง)**

```lua
   local pad = script.Parent

pad.Touched:Connect(function(otherPart)
	local character = otherPart.Parent
	local root = character:FindFirstChild("HumanoidRootPart")
	if root then
		root.Velocity = Vector3.new(0, 80, 0)
	end
end)
```
