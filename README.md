# ROBLOX Script

1. **Kill Block (Dødskloss / Смертельний блок / แผ่นอันตราย)**

- 🇬🇧: Instantly kills the player upon touch.
- 🇳🇴: Dreper spilleren umiddelbart ved berøring.
- 🇺🇦: Миттєво вбиває гравця при доторку.
- 🇹🇭: ทำให้ตัวละครตายทันทีเมื่อสัมผัส

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

2. **Disappearing Block (Forsvinnende kloss / Зникаючий блок / แผ่นหายตัว)**

- 🇬🇧: Block becomes invisible and non-solid shortly after being touched.
- 🇳🇴: Klossen blir usynlig og umulig å stå på en kort stund etter berøring.
- 🇺🇦: Блок стає невидимим і не проходить крізь нього короткий час після доторку.
- 🇹🇭: แผ่นจะจางหายและทะลุได้ชั่วคราวเมื่อเหยียบ

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

3. **Speed Boost (Fartsøkning / Прискорення / แผ่นเพิ่มความเร็ว)**

- 🇬🇧: Temporarily increases the player's walking speed.
- 🇳🇴: Gir spilleren raskere gåfart midlertidig.
- 🇺🇦: Тимчасово збільшує швидкість ходьби гравця.
- 🇹🇭: เพิ่มความเร็วในการเดินชั่วคราว

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

4. **High Jump Pad (Hoppepute / Стрибкова подушка / แผ่นเด้งสูง)**

- 🇬🇧: Launches the player into the air using a velocity vector.
- 🇳🇴: Sender spilleren opp i luften med en hastighetsvektor.
- 🇺🇦: Підкидає гравця в повітря за допомогою вектора швидкості.
- 🇹🇭: ส่งตัวละครกระโดดลอยขึ้นฟ้าด้วยเวกเตอร์ความเร็ว

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

5. **Rotating Obstacle (Roterende hindring / แท่งหมุนสิ่งกีดขวาง)**

```lua
local part = script.Parent

while true do
	part.CFrame = part.CFrame * CFrame.Angles(0, math.rad(5), 0)
	task.wait(0.03)
end
```

6. **Teleporter (Teleportering / วาร์ปไปจุดต่อไป)**

```lua
local portal = script.Parent

portal.Touched:Connect(function(otherPart)
	local character = otherPart.Parent
	local root = character:FindFirstChild("HumanoidRootPart")
	local target = workspace:FindFirstChild("TeleportTarget")
	
	if root and target then
		root.CFrame = target.CFrame + Vector3.new(0, 3, 0)
	end
end)
```

7. **
