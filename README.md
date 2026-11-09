# ROBLOX Script

---

0. **Checkpoint Script (Sjekkpunkt / Контрольна точка / จุดบันทึกจุดเกิด)**

- 🇬🇧: Updates the player's spawn location to this block upon touch.
- 🇳🇴: Oppdaterer spillere-s spawn-lokasjon til denne klossen ved berøring.
- 🇺🇦: Змінює точку появи гравця на цей блок при доторку.
- 🇹🇭: อัปเดตจุดเกิดของผู้เล่นมาที่แผ่นนี้เมื่อสัมผัส

```lua
local checkpoint = script.Parent

checkpoint.Touched:Connect(function(otherPart)
	local character = otherPart.Parent
	local player = game.Players:GetPlayerFromCharacter(character)
	
	if player then
		player.RespawnLocation = checkpoint
	end
end)
```
***How to set it up in Roblox Studio:***

Insert a Part where you want the checkpoint to be.
In the Properties window, make sure Anchored is set to true.
Insert a standard Script inside that Part and paste the code above.

---

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

---

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

---

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

---

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

---

5. **Rotating Obstacle (Roterende hindring / แท่งหมุนสิ่งกีดขวาง)**

- 🇬🇧: Continuously rotates the part around its axis.
- 🇳🇴: Roterer klossen kontinuerlig rundt sin akse.
- 🇺🇦: Безперервно обертає блок навколо своєї осі.
- 🇹🇭: หมุนชิ้นส่วนไปเรื่อยๆ อย่างต่อเนื่อง

```lua

local part = script.Parent

while true do
	part.CFrame = part.CFrame * CFrame.Angles(0, math.rad(5), 0)
	task.wait(0.03)
end
```

---

6. **Teleporter (Teleportering / วาร์ปไปจุดต่อไป)**

- 🇬🇧: Instantly moves the player to a target location in the game world.
- 🇳🇴: Flytter spilleren umiddelbart til et annet mål i spillverdenen.
- 🇺🇦: Миттєво переміщує гравця до іншої цілі у світі гри.
- 🇹🇭: ย้ายตำแหน่งตัวละครไปยังจุดปลายทางทันที

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

---

7. **Lava Floor (Lava-gulv / Лавова підлога / แผ่นลาวาค่อยๆ ลดเลือด)**

- 🇬🇧: Gradually damages the player while standing on the block.
- 🇳🇴: Skader spilleren gradvis så lenge de står på klossen.
- 🇺🇦: Поступово завдає шкоди гравцю, поки він стоїть на блоці.
- 🇹🇭: ค่อยๆ ลดเลือดเรื่อยๆ ตราบใดที่ยังยืนบนแผ่นนี้

```lua
local lavaPart = script.Parent

lavaPart.Touched:Connect(function(otherPart)
	local character = otherPart.Parent
	local humanoid = character:FindFirstChildOfClass("Humanoid")
	if humanoid and humanoid.Health > 0 then
		humanoid:TakeDamage(10)
		task.wait(0.5)
	end
end)
```

---

8. **Conveyor Belt (Samlebånd / Конвеєрна стрічка / สายพานเลื่อนตัวละคร)**

- 🇬🇧: Automatically pushes the player in a specific direction.
- 🇳🇴: Skyver spilleren i en bestemt retning automatisk.
- 🇺🇦: Автоматично штовхає гравця в певному напрямку.
- 🇹🇭: ดันตัวละครให้เคลื่อนที่ไปตามทิศทางอัตโนมัติ

```lua
local conveyor = script.Parent

conveyor.AssemblyLinearVelocity = conveyor.CFrame.LookVector * 25
```

---

9. **Trampoline (Super-trampoline / Батут / แผ่นสปริงเด้งดึ๋ง)**

- 🇬🇧: Launches the player upward using an impulse force.
- 🇳🇴: Skyter spilleren oppover ved hjelp av impuls-kraft.
- 🇺🇦: Підкидає гравця вгору за допомогою імпульсної сили.
- 🇹🇭: ดีดตัวผู้เล่นขึ้นด้านบนด้วยแรงกระแทก

```lua
local pad = script.Parent

pad.Touched:Connect(function(otherPart)
	local character = otherPart.Parent
	local root = character:FindFirstChild("HumanoidRootPart")
	if root then
		root:ApplyImpulse(Vector3.new(0, 2500, 0))
	end
end)
```

---

10. **Coin Collector (Mynt-samler / Збір монет / เหรียญเก็บสะสม)**

- 🇬🇧: Awards points to the player and temporarily vanishes before respawning.
- 🇳🇴: Gir poeng til spilleren og forsvinner midlertidig før den dukker opp igjen.
- 🇺🇦: Нараховує очки гравцю та тимчасово зникає перед відновленням.
- 🇹🇭: เพิ่มคะแนนให้ผู้เล่นและเหรียญจะหายไปชั่วคราวก่อนเกิดใหม่

```lua
local coin = script.Parent
local isCollected = false

coin.Touched:Connect(function(otherPart)
	local character = otherPart.Parent
	local player = game.Players:GetPlayerFromCharacter(character)
	
	if player and not isCollected then
		isCollected = true
		if player:FindFirstChild("leaderstats") and player.leaderstats:FindFirstChild("Coins") then
			player.leaderstats.Coins.Value += 1
		end
		coin.Transparency = 1
		coin.CanCollide = false
		task.wait(5)
		coin.Transparency = 0
		coin.CanCollide = true
		isCollected = false
	end
end)
```

---

11. **Falling Floor (Fellende gulv / Падаюча підлога / พื้นใต้เท้าหล่น)**

- 🇬🇧: The floor unanchors and falls down when stepped on.
- 🇳🇴: Gulvet mister forankringen og faller ned når spilleren tråkker på det.
- 🇺🇦: Підлога втрачає закріплення і падає, коли на неї наступають.
- 🇹🇭: พื้นจะหลุดร่วงตกลงมาเมื่อผู้เล่นเหยียบ

```lua
local trapDoor = script.Parent
local triggered = false

trapDoor.Touched:Connect(function(otherPart)
	local character = otherPart.Parent
	if character:FindFirstChildOfClass("Humanoid") and not triggered then
		triggered = true
		task.wait(0.5)
		trapDoor.Anchored = false
		task.wait(3)
		trapDoor.AssemblyLinearVelocity = Vector3.zero
		trapDoor.AssemblyAngularVelocity = Vector3.zero
		trapDoor.Anchored = true
		triggered = false
	end
end)
```

---

12. **Checkpoint Flag (Sjekkpunkt-flagg / Прапорець збереження / ธงบันทึกจุดเกิด)**

- 🇬🇧: Updates the player's spawn location to this block upon touch
- 🇳🇴: Endrer spillerens spawn-lokasjon til denne klossen ved berøring.
- 🇺🇦: Змінює точку появи гравця на цей блок при доторку..
- 🇹🇭: อัปเดตจุดเกิดของผู้เล่นมาที่แผ่นนี้เมื่อสัมผัส

```lua
local checkpoint = script.Parent

checkpoint.Touched:Connect(function(otherPart)
	local character = otherPart.Parent
	local player = game.Players:GetPlayerFromCharacter(character)
	
	if player then
		player.RespawnLocation = checkpoint
	end
end)
```

---

13. **Low Gravity Zone (Lav tyngdekraft / Зона низької гравітації / โซนแรงโน้มถ่วงต่ำ)**

- 🇬🇧: Temporarily allows the player to jump much higher.
- 🇳🇴: Gir spilleren mulighet til å hoppe mye høyere midlertidig.
- 🇺🇦: Дозволяє гравцеві стрибати набагато вище тимчасово.
- 🇹🇭: ทำให้ผู้เล่นกระโดดได้สูงขึ้นมากชั่วคราว

```lua
local zone = script.Parent

zone.Touched:Connect(function(otherPart)
	local character = otherPart.Parent
	local humanoid = character:FindFirstChildOfClass("Humanoid")
	if humanoid then
		humanoid.UseJumpPower = true
		humanoid.JumpPower = 100
	end
end)
```

---

14. **Reset Jump Pad (Nullstill hopp / Скидання стрибка / แผ่นรีเซ็ตการกระโดด)**

- 🇬🇧: Resets the player's jump power back to the default value.
- 🇳🇴: Tilbakestiller spillerens hoppekraft til standardverdi.
- 🇺🇦: Повертає силу стрибка гравця до стандартного значення.
- 🇹🇭: คืนค่าพลังการกระโดดของผู้เล่นให้กลับมาเป็นค่าปกติ

```lua
local pad = script.Parent

pad.Touched:Connect(function(otherPart)
	local character = otherPart.Parent
	local humanoid = character:FindFirstChildOfClass("Humanoid")
	if humanoid then
		humanoid.JumpPower = 50
	end
end)
```

15. **Blinking Block (Blinkende kloss / Миготливий блок / แผ่นกะพริบเปิด-ปิด)**

