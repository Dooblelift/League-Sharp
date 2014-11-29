using System;
using System.Collections;
using System.Linq;

using LeagueSharp;
using LeagueSharp.Common;
using SharpDX;
using Color = System.Drawing.Color;
using System.Collections.Generic;
using System.Threading;

namespace Vanilla
{
    class Program
    {
        private static Obj_AI_Hero Player { get { return ObjectManager.Player; } }

        private static Orbwalking.Orbwalker Orbwalker;

        private static Spell Q,W,E,R;

        private static Items.Item Dfg;

        private static Menu Menu;

        static void Main(string[] args)
        {CustomEvents.Game.OnGameLoad += Game_OnGameLoad;
        }
        private static void Game_OnGameLoad(EventArgs args)
        {
            if (Player.ChampionName != "Veigar")
                return;

            Q= new Spell(SpellSlot.Q,650);
            W= new Spell(SpellSlot.W,900);
            E= new Spell(SpellSlot.E,650);
            R= new Spell(SpellSlot.R,650);

            W.SetSkillshot(1.25f, 225, float.MaxValue, false, SkillshotType.SkillshotCircle);

            Dfg = new Items.Item(3128, 750);

            Menu = new Menu(Player.ChampionName, Player.ChampionName, true);

            Menu orbwalkerMenu = Menu.AddSubMenu(new Menu("Orbwalker", "Orbwalker"));

            Menu ts = Menu.AddSubMenu(new Menu("Target Selector", "Target Selector"));

            SimpleTs.AddToMenu(ts);

            Menu spellMenu = Menu.AddSubMenu(new Menu("Spells", "Spells"));

            spellMenu.AddItem(new MenuItem("useQ", "Use Q").SetValue(true));
            spellMenu.AddItem(new MenuItem("useW", "Use W").SetValue(true));
            spellMenu.AddItem(new MenuItem("useE", "Use E").SetValue(true));
            spellMenu.AddItem(new MenuItem("useR", "Use R").SetValue(true));

            Menu.AddToMainMenu();

            Drawing.OnDraw += Drawing_OnDraw;

            Game.OnGameUpdate += Game_OnGameUpdate;

            Game.PrintChat("Vanilla Veigar");
        }
        private static void Game_OnGameUpdate(EventArgs args)
        {
            if(Player.IsDead)
                return;

            if (Orbwalker.ActiveMode == Orbwalking.OrbwalkingMode.Combo)
            {
                Stun();
                Darkmatter();
                Baleful();
                Primburst();
            }

            if (Orbwalker.ActiveMode == Orbwalking.OrbwalkingMode.Mixed)
            {
                Baleful();
            }

            if (Orbwalker.ActiveMode == Orbwalking.OrbwalkingMode.LaneClear)
            {
                Darkmatter();
                Baleful();
            }
        }
            private static void Drawing_OnDraw(EventArgs args)
            {
                if (Player.IsDead)
                    return;

                if (E.IsReady())
                {
                    Utility.DrawCircle(Player.Position, E.Range, Color.Aqua);
                }
                else
                {
                    Utility.DrawCircle(Player.Position, E.Range, Color.DarkRed);
                }
            }
        private static void Baleful()
        {
            
            if (Q.IsReady())
            {
                var target = SimpleTs.GetTarget(E.Range, SimpleTs.DamageType.Magical);
                if (target == null)
                    return;
                {
                    Q.CastOnUnit(target);
                }

                }
        }

        private static void Darkmatter()
        {
            if (W.IsReady())
            {
                var target = SimpleTs.GetTarget(E.Range, SimpleTs.DamageType.Magical);
                if (target == null)
                    return;
                {
                    W.CastOnUnit(target);
                }
            }
        }
        
        private static void Stun() 
        {
        if (E.IsReady())
        {
            var target = SimpleTs.GetTarget(E.Range, SimpleTs.DamageType.Magical);
                if (target == null)
                    return;
            var prediction = E.GetPrediction(target);
                {
                    E.CastOnUnit(target);
                    }
                }
            }
        private static void Primburst()
        {
            if (R.IsReady())
            {
                var target = SimpleTs.GetTarget(E.Range, SimpleTs.DamageType.Magical);
                if (target == null)
                    return;
                {
                    R.CastOnUnit(target);
                }
            }
        }
    }
}
