--[[
	Auto Idle Logo Script for AZ-MPV
	Displays portable_config/logo.jpg when player is idle.
]]

local utils = require("mp.utils")
local logo_path = mp.command_native({"expand-path", "~~/logo.jpg"})
local is_loading = false

local function load_logo()
	if is_loading then return end
	local current_path = mp.get_property("path")
	if not current_path or current_path == "" then
		is_loading = true
		mp.commandv("loadfile", logo_path, "replace")
		mp.set_property("pause", "yes")
		is_loading = false
	end
end

mp.register_event("idle", function()
	load_logo()
end)

mp.register_event("end-file", function(event)
	if event.reason == "eof" or event.reason == "stop" or event.reason == "error" then
		mp.add_timeout(0.05, function()
			local current_path = mp.get_property("path")
			if not current_path or current_path == "" then
				load_logo()
			end
		end)
	end
end)

mp.add_timeout(0.1, function()
	local current_path = mp.get_property("path")
	if not current_path or current_path == "" then
		load_logo()
	end
end)
