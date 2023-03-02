<?php

namespace AzniDev\SimpleGamemode;

use pocketmine\player\Player;
use poxketmine\player\GameMode;
use pocketmine\plugin\PluginBase;
use pocketmine\utils\SingletonTrait;
use pocketmine\command\Command;
use pocketmine\command\CommandSender;

class SimpleGamemode extends PLuginBase {
    use SingletonTrait;
    
    public function onEnable(): void {
        self::setInstance($this);
    }
    
    public function onCommand(CommandSender $sender, Command $cmd, String $label, Array $args): bool {
        switch(strtolower($cmd->getName())) {
            case "gms":
                if(isset($args[0]) && $sender->hasPermission("simplegamemode.gms.other")) {
                    $target = $this->getServer()->getPlayerByPrefix($args[0]);
                    $this->setGamemode($target, "survival");
                }
                if($sender instanceof Player) {
                    $this->setGamemode($sender, "survival");
                }
            break;
            case "gmc":
                if(isset($args[0]) && $sender->hasPermission("simplegamemode.gmc.other")) {
                    $target = $this->getServer()->getPlayerByPrefix($args[0]);
                    $this->setGamemode($target, "creative");
                }
                if($sender instanceof Player) {
                    $this->setGamemode($sender, "creative");
                }
            break;
            case "gma":
                if(isset($args[0]) && $sender->hasPermission("simplegamemode.gma.other")) {
                    $target = $this->getServer()->getPlayerByPrefix($args[0]);
                    $this->setGamemode($target, "adventure");
                }
                if($sender instanceof Player) {
                    $this->setGamemode($sender, "adventure");
                }
            break;
            case "gmsp":
                if(isset($args[0]) && $sender->hasPermission("simplegamemode.gmsp.other")) {
                    $target = $this->getServer()->getPlayerByPrefix($args[0]);
                    $this->setGamemode($target, "spectator");
                }
                if($sender instanceof Player) {
                    $this->setGamemode($sender, "spectator");
                }
            break;
        }
        return true;
    }
    
    public function setGamemode(Player $player, string $gamemode) {
        if(!$player->isOnline()) return;
        switch(strtolower($gamemode)) {
            case "survival":
                $player->setGamemode(GameMode::SURVIVAL());
            break;
            case "creative":
                $player->setGamemode(GameMode::CREATIVE());
            break;
            case "adventure":
                $player->setGamemode(GameMode::ADVENTURE());
            break;
            case "spectator":
                $player->setGamemode(GameMode::SPECTATOR());
            break;
        }
    }
}
