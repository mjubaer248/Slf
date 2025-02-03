# Slf
require('dotenv').config();
const { Telegraf, Markup } = require('telegraf');

const bot = new Telegraf(process.env.BOT_TOKEN);

bot.start((ctx) => {
    ctx.reply("🤖 Welcome! Click the button and see ads!", getClickButton());
});

// Self Click Button + Ads
function getClickButton() {
    return Markup.inlineKeyboard([
        [Markup.button.callback("🔄 Auto Click", "auto_click")],
        [Markup.button.url("🔥 Sponsor: Click Here", "https://your-ad-link.com")]
    ]);
}

bot.action("auto_click", (ctx) => {
    ctx.answerCbQuery("✅ Button clicked!");

    // ✅ **Show an ad after every click**
    ctx.reply("📢 **Sponsored Ad:** 🔥 **Special Offer!**\n👉 [Visit Now](https://your-ad-link.com)", { parse_mode: "Markdown" });

    setTimeout(() => {
        ctx.editMessageText("♻️ Auto-clicking...", getClickButton());
    }, 2000);
});

bot.launch();
console.log("🚀 Bot is running...");
