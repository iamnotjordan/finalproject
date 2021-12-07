local Monster = script.Parent

Monster.Humanoid.Touched:Connect(function(hit)
	if hit and game.Players:GetPlayerFromCharacter(hit.Parent) then
		hit.Parent.Humanoid:TakeDamage(100)
	end
end)

function FindPlayer(Position)
	local List = game.Workspace:GetChildren()
	local Torso = nil
	local Distance = 100000
	local HumanoidRootPart = nil
	local Humanoid = nil
	local Player = nil

	for i = 1, #List do
		Player = List[i]
		if (Player.ClassName == "Model") and (Player ~= script.Parent) then
			HumanoidRootPart = Player:FindFirstChild("HumanoidRootPart")
			Humanoid = Player:FindFirstChild("Humanoid")
			if (HumanoidRootPart ~= nil) and (Humanoid ~= nil) and (Humanoid.Health > 0) then
				if (HumanoidRootPart.Position - Position).Magnitude < Distance then
					Torso = HumanoidRootPart
					Distance = (HumanoidRootPart.Position - Position).Magnitude
				end
			end
		end
	end
	return Torso
end

while true do
	wait(1)
	local Target = FindPlayer(script.Parent.HumanoidRootPart.Position)
	if Target ~= nil then
		script.Parent.Humanoid:MoveTo(Target.Position, Target)
	end
end

References:
# https://devforum.roblox.com/t/humanoid-damage-script-error/1020107
# https://scriptinghelpers.org/questions/89144/scripting-an-enemy-that-follows-a-player
