const http = require('http');
const crypto = require('crypto');
const { Client, GatewayIntentBits, REST, Routes, SlashCommandBuilder, EmbedBuilder } = require('discord.js');

// 1. Health-check HTTP Server for Render Dashboard
const PORT = process.env.PORT || 10000;
const STATS = {
  startTime: Date.now(),
  totalChecked: 0,
  availableFound: 0,
  lastFound: 'None yet',
  currentDelay: 2000
};

http.createServer((req, res) => {
  const uptimeHours = ((Date.now() - STATS.startTime) / (1000 * 60 * 60)).toFixed(2);
  res.writeHead(200, { 'Content-Type': 'text/html' });
  res.end(`
    <!DOCTYPE html>
    <html>
    <head>
      <title>Cool Username Scanner Dashboard</title>
      <meta http-equiv="refresh" content="10">
      <style>
        body { font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif; background: #0f172a; color: #f8fafc; display: flex; justify-content: center; align-items: center; min-height: 100vh; margin: 0; }
        .card { background: #1e293b; padding: 2rem; border-radius: 12px; box-shadow: 0 10px 25px rgba(0,0,0,0.5); width: 100%; max-width: 450px; border: 1px solid #334155; }
        h1 { margin-top: 0; font-size: 1.4rem; color: #38bdf8; display: flex; align-items: center; justify-content: space-between; }
        .grid { display: grid; grid-template-columns: 1fr 1fr; gap: 1rem; margin-top: 1rem; }
        .box { background: #0f172a; padding: 1rem; border-radius: 8px; border: 1px solid #334155; }
        .val { font-size: 1.3rem; font-weight: bold; margin-top: 0.2rem; }
        .green { color: #4ade80; }
        .sub { font-size: 0.75rem; color: #94a3b8; text-transform: uppercase; letter-spacing: 0.05em; }
      </style>
    </head>
    <body>
      <div class="card">
        <h1>Aesthetic Username Scanner <span>🟢 ONLINE</span></h1>
        <div class="grid">
          <div class="box"><div class="sub">Total Checked</div><div class="val">${STATS.totalChecked}</div></div>
          <div class="box"><div class="sub">Available Found</div><div class="val green">${STATS.availableFound}</div></div>
          <div class="box"><div class="sub">Uptime</div><div class="val">${uptimeHours} hrs</div></div>
          <div class="box"><div class="sub">Check Speed</div><div class="val">${(STATS.currentDelay / 1000).toFixed(1)}s</div></div>
        </div>
        <div class="box" style="margin-top:1rem;">
          <div class="sub">Last Cool Name Found</div>
          <div class="val green">${STATS.lastFound}</div>
        </div>
      </div>
    </body>
    </html>
  `);
}).listen(PORT, () => {
  console.log(`[HTTP Server] Live on port ${PORT}`);
});

// 2. Configuration & State Management
const CONFIG = {
  mode: process.env.SCAN_MODE || 'all_cool',
  discordToken: process.env.DISCORD_BOT_TOKEN || '',
  mainChannelId: process.env.DISCORD_MAIN_CHANNEL_ID || '',
  historyChannelId: process.env.DISCORD_HISTORY_CHANNEL_ID || '',
  autoClaimEnabled: process.env.AUTO_CLAIM === 'true',
  baseDelayMs: 2000
};

const seenUsernames = new Set();
const lifetimeHistory = [];

// Curated Wordlists for Clean, Cool, and Normal Usernames
const DICTIONARY = {
  prefixes: [
    "real", "its", "iam", "the", "just", "not", "sir", "lord", "dr", "saint",
    "pure", "neo", "hyper", "cyber", "lunar", "solar", "astro", "velvet", "sub", "super"
  ],
  suffixes: [
    "zone", "mode", "core", "wave", "vibe", "flow", "pulse", "craft", "lab", "hub",
    "realm", "verse", "vault", "hq", "space", "club", "life", "drift", "park", "fx"
  ],
  coolNouns: [
    "shadow", "phantom", "echo", "frost", "ember", "storm", "drift", "hollow", "apex",
    "vortex", "cipher", "zenith", "mirage", "prism", "spectre", "orbit", "aura", "haven",
    "summit", "oasis", "signal", "vector", "static", "glitch", "flame", "horizon", "spirit"
  ],
  aestheticWords: [
    "velvet", "cosmic", "lunar", "stellar", "golden", "silent", "frozen", "radiant",
    "crimson", "subtle", "hollow", "astral", "dusk", "dawn", "cloud", "clover", "ocean"
  ],
  shortNames: [
    "cody", "liam", "noah", "kai", "ezra", "leo", "zane", "finn", "milo", "nico",
    "elena", "maya", "ivy", "chloe", "nova", "aria", "sora", "remi", "cleo", "zoe"
  ],
  gamerTags: [
    "blade", "viper", "striker", "hunter", "scout", "ranger", "titan", "rogue",
    "ghost", "venom", "fury", "spark", "pulse", "raider", "reaper", "sentry"
  ]
};

// Helper function to capitalize first letter
function capitalize(str) {
  return str.charAt(0).toUpperCase() + str.slice(1);
}

// 3. Normal & Cool Username Generators
function generateCandidate(selectedMode) {
  let mode = selectedMode;
  if (mode === 'all_cool') {
    const modes = ['compound_cool', 'clean_prefix', 'aesthetic_two_word', 'short_name_tag', 'gamer_handle', 'clean_suffix'];
    mode = modes[Math.floor(Math.random() * modes.length)];
  }

  // Example: EchoPulse, ShadowVortex, FrostHaven
  if (mode === 'compound_cool') {
    const word1 = DICTIONARY.coolNouns[Math.floor(Math.random() * DICTIONARY.coolNouns.length)];
    let word2 = DICTIONARY.suffixes[Math.floor(Math.random() * DICTIONARY.suffixes.length)];
    if (Math.random() > 0.5) {
      word2 = DICTIONARY.coolNouns[Math.floor(Math.random() * DICTIONARY.coolNouns.length)];
    }
    const name = Math.random() > 0.5 ? `${word1}${word2}` : `${capitalize(word1)}${capitalize(word2)}`;
    return { name, genre: "Compound Cool" };
  }

  // Example: RealPhantom, ItsAura, JustEcho, NeoApex
  if (mode === 'clean_prefix') {
    const pre = DICTIONARY.prefixes[Math.floor(Math.random() * DICTIONARY.prefixes.length)];
    const noun = DICTIONARY.coolNouns[Math.floor(Math.random() * DICTIONARY.coolNouns.length)];
    const name = Math.random() > 0.5 ? `${pre}${noun}` : `${capitalize(pre)}${capitalize(noun)}`;
    return { name, genre: "Prefix + Cool Word" };
  }

  // Example: CosmicDrift, VelvetFlame, LunarHorizon
  if (mode === 'aesthetic_two_word') {
    const adj = DICTIONARY.aestheticWords[Math.floor(Math.random() * DICTIONARY.aestheticWords.length)];
    const noun = DICTIONARY.coolNouns[Math.floor(Math.random() * DICTIONARY.coolNouns.length)];
    const name = Math.random() > 0.5 ? `${adj}${noun}` : `${capitalize(adj)}${capitalize(noun)}`;
    return { name, genre: "Aesthetic Two-Word" };
  }

  // Example: KaiVibes, MiloFlow, EzraCore, IvyZone
  if (mode === 'short_name_tag') {
    const nameBase = DICTIONARY.shortNames[Math.floor(Math.random() * DICTIONARY.shortNames.length)];
    const suf = DICTIONARY.suffixes[Math.floor(Math.random() * DICTIONARY.suffixes.length)];
    const name = Math.random() > 0.5 ? `${nameBase}${suf}` : `${capitalize(nameBase)}${capitalize(suf)}`;
    return { name, genre: "Short Name Handle" };
  }

  // Example: GhostViper, StrikerPulse, BladeRanger
  if (mode === 'gamer_handle') {
    const g1 = DICTIONARY.gamerTags[Math.floor(Math.random() * DICTIONARY.gamerTags.length)];
    let g2 = DICTIONARY.gamerTags[Math.floor(Math.random() * DICTIONARY.gamerTags.length)];
    while (g1 === g2) {
      g2 = DICTIONARY.gamerTags[Math.floor(Math.random() * DICTIONARY.gamerTags.length)];
    }
    const name = Math.random() > 0.5 ? `${g1}${g2}` : `${capitalize(g1)}${capitalize(g2)}`;
    return { name, genre: "Clean Gamer Tag" };
  }

  // Example: ApexHQ, VortexRealm, MirageVault
  if (mode === 'clean_suffix') {
    const noun = DICTIONARY.coolNouns[Math.floor(Math.random() * DICTIONARY.coolNouns.length)];
    const suf = DICTIONARY.suffixes[Math.floor(Math.random() * DICTIONARY.suffixes.length)];
    const name = Math.random() > 0.5 ? `${noun}${suf}` : `${capitalize(noun)}${capitalize(suf)}`;
    return { name, genre: "Word + Suffix" };
  }

  return { name: "RealShadow", genre: "Default" };
}

// 4. Auto-Signup Module (0 Robux)
function generateRandomPassword() {
  return 'Rbx!' + crypto.randomBytes(6).toString('hex') + '99';
}

async function claimUsernameOnRoblox(username) {
  const password = generateRandomPassword();

  try {
    const signupRes = await fetch("https://auth.roblox.com/v2/signup", {
      method: "POST",
      headers: {
        'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36',
        'Content-Type': 'application/json'
      },
      body: JSON.stringify({
        username: username,
        password: password,
        birthday: "2000-01-01",
        gender: 2,
        isRbxIsUnder13: false
      })
    });

    const data = await signupRes.json();

    if (signupRes.ok && data.userId) {
      return {
        success: true,
        username: username,
        password: password,
        userId: data.userId
      };
    } else {
      const errReason = data.errors?.[0]?.message || `HTTP ${signupRes.status}`;
      return { success: false, reason: errReason };
    }
  } catch (err) {
    return { success: false, reason: err.message };
  }
}

// 5. Roblox Username Availability Checker
async function checkUsername(username) {
  const customHeaders = {
    'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36',
    'Content-Type': 'application/json'
  };

  try {
    const userCheckRes = await fetch("https://users.roblox.com/v1/usernames/users", {
      method: "POST",
      headers: customHeaders,
      body: JSON.stringify({ usernames: [username], excludeBannedUsers: false })
    });

    if (userCheckRes.status === 429) return 'ratelimit';
    if (userCheckRes.ok) {
      const userData = await userCheckRes.json();
      if (userData.data && userData.data.length > 0) return 'taken';
    }

    const validateRes = await fetch("https://auth.roblox.com/v1/usernames/validate", {
      method: "POST",
      headers: customHeaders,
      body: JSON.stringify({ username, birthday: "2000-01-01" })
    });

    if (validateRes.status === 429) return 'ratelimit';
    if (validateRes.ok) {
      const valData = await validateRes.json();
      if (valData.code === 0) return 'available';
    }

    return 'taken';
  } catch (err) {
    return 'error';
  }
}

// 6. Discord Bot Client & Slash Commands Setup
const discordClient = new Client({ intents: [GatewayIntentBits.Guilds] });

const slashCommands = [
  new SlashCommandBuilder().setName('status').setDescription('View live status and scan statistics'),
  new SlashCommandBuilder().setName('mode').setDescription('Change the cool username generator mode')
    .addStringOption(opt => opt.setName('genre').setDescription('Choose genre')
      .setRequired(true)
      .addChoices(
        { name: 'All Cool Modes', value: 'all_cool' },
        { name: 'Compound Cool (e.g. EchoPulse)', value: 'compound_cool' },
        { name: 'Prefix + Cool Word (e.g. RealPhantom)', value: 'clean_prefix' },
        { name: 'Aesthetic Two-Word (e.g. CosmicDrift)', value: 'aesthetic_two_word' },
        { name: 'Short Name Handle (e.g. KaiVibes)', value: 'short_name_tag' },
        { name: 'Clean Gamer Tag (e.g. GhostViper)', value: 'gamer_handle' },
        { name: 'Word + Suffix (e.g. ApexHQ)', value: 'clean_suffix' }
      )),
  new SlashCommandBuilder().setName('history').setDescription('View lifetime found cool usernames')
];

discordClient.on('interactionCreate', async interaction => {
  if (!interaction.isChatInputCommand()) return;

  if (interaction.commandName === 'status') {
    const uptime = ((Date.now() - STATS.startTime) / (1000 * 60 * 60)).toFixed(2);
    const embed = new EmbedBuilder()
      .setTitle("📊 Cool Username Scanner Status")
      .setColor(0x38bdf8)
      .addFields(
        { name: "Total Checked", value: `${STATS.totalChecked}`, inline: true },
        { name: "Available Found", value: `${STATS.availableFound}`, inline: true },
        { name: "Current Mode", value: `\`${CONFIG.mode}\``, inline: true },
        { name: "Uptime", value: `${uptime} hours`, inline: true },
        { name: "Auto-Claimer (0-Robux)", value: CONFIG.autoClaimEnabled ? "🟢 ENABLED" : "🔴 DISABLED", inline: true },
        { name: "Unique Memory", value: `${seenUsernames.size} names`, inline: true }
      );
    await interaction.reply({ embeds: [embed] });
  }

  if (interaction.commandName === 'mode') {
    const newMode = interaction.options.getString('genre');
    CONFIG.mode = newMode;
    await interaction.reply(`✅ Generator mode updated to **\`${newMode}\`**!`);
  }

  if (interaction.commandName === 'history') {
    if (lifetimeHistory.length === 0) {
      return interaction.reply("📜 Lifetime History is currently empty. No available names found yet.");
    }
    const historyList = lifetimeHistory.slice(-15).map((item, idx) => `${idx + 1}. \`${item.name}\` (${item.genre}) - *<t:${Math.floor(item.time / 1000)}:R>*`).join("\n");
    const embed = new EmbedBuilder()
      .setTitle("📜 Lifetime Username History (Recent 15)")
      .setDescription(historyList)
      .setColor(0x4ade80);
    await interaction.reply({ embeds: [embed] });
  }
});

// 7. Dispatch Alerts (Main + Lifetime History Channels)
async function dispatchAlert(candidate, claimResult) {
  if (CONFIG.mainChannelId) {
    const channel = await discordClient.channels.fetch(CONFIG.mainChannelId).catch(() => null);
    if (channel) {
      if (CONFIG.autoClaimEnabled && claimResult.success) {
        const embed = new EmbedBuilder()
          .setTitle("🎉 NEW COOL ACCOUNT CREATED!")
          .setDescription(`The bot successfully registered this cool username for **0 Robux**!`)
          .setColor(0x00FF00)
          .addFields(
            { name: "👤 Username", value: `\`${claimResult.username}\``, inline: true },
            { name: "🔑 Generated Password", value: `||\`${claimResult.password}\`|| *(Click to reveal)*`, inline: true },
            { name: "🆔 User ID", value: `\`${claimResult.userId}\``, inline: true },
            { name: "🎭 Name Style", value: `\`${candidate.genre}\``, inline: true }
          )
          .setFooter({ text: "Log in immediately at Roblox.com and change the password!" })
          .setTimestamp();

        await channel.send({ content: "🚨 **NEW COOL USERNAME CLAIMED!** 🚨", embeds: [embed] });
      } else {
        const embed = new EmbedBuilder()
          .setTitle("🚨 COOL USERNAME UNLOCKED!")
          .setDescription(`**Username:** \`${candidate.name}\`\n**Style:** \`${candidate.genre}\`\n**Length:** \`${candidate.name.length} Characters\``)
          .setColor(CONFIG.autoClaimEnabled ? 0xFFA500 : 0x00FF00)
          .addFields(
            { 
              name: "⚡ Quick Claim Link", 
              value: `[Click Here to Register on Roblox](https://www.roblox.com/CreateAccount?returnUrl=https%3A%2F%2Fwww.roblox.com%2F%3Fnl%3Dtrue)` 
            }
          )
          .setTimestamp();

        if (CONFIG.autoClaimEnabled && !claimResult.success) {
          embed.addFields({ name: "⚠️ Auto-Claim Status", value: `Failed: \`${claimResult.reason}\` (Manual signup required)` });
        }

        await channel.send({ embeds: [embed] });
      }
    }
  }

  if (CONFIG.historyChannelId) {
    const histChannel = await discordClient.channels.fetch(CONFIG.historyChannelId).catch(() => null);
    if (histChannel) {
      const histEmbed = new EmbedBuilder()
        .setTitle("📜 History Entry")
        .setDescription(`\`${candidate.name}\` | **Style:** ${candidate.genre} | **Time:** <t:${Math.floor(Date.now() / 1000)}:F>`)
        .setColor(0x38bdf8);
      histChannel.send({ embeds: [histEmbed] });
    }
  }
}

// 8. Scanner Loop
async function startScanner() {
  console.log("🚀 Cool Roblox Username Scanner Booting...");

  if (CONFIG.discordToken) {
    try {
      await discordClient.login(CONFIG.discordToken);
      console.log(`🤖 Logged into Discord as ${discordClient.user.tag}`);

      const rest = new REST().setToken(CONFIG.discordToken);
      await rest.put(
        Routes.applicationCommands(discordClient.user.id),
        { body: slashCommands }
      );
      console.log("⚡ Discord Slash Commands Registered!");
    } catch (e) {
      console.error("Discord Login Error:", e.message);
    }
  }

  while (true) {
    try {
      let candidate;
      do {
        candidate = generateCandidate(CONFIG.mode);
      } while (seenUsernames.has(candidate.name));

      seenUsernames.add(candidate.name);

      const status = await checkUsername(candidate.name);

      if (status === 'available') {
        STATS.availableFound++;
        STATS.lastFound = `${candidate.name} (${candidate.genre})`;
        lifetimeHistory.push({ name: candidate.name, genre: candidate.genre, time: Date.now() });

        console.log(`\x1b[32m[AVAILABLE] ${candidate.name} (${candidate.genre})\x1b[0m`);

        let claimResult = { success: false, reason: "Disabled" };
        if (CONFIG.autoClaimEnabled) {
          claimResult = await claimUsernameOnRoblox(candidate.name);
        }

        await dispatchAlert(candidate, claimResult);
        STATS.currentDelay = CONFIG.baseDelayMs;
      } else if (status === 'taken') {
        STATS.totalChecked++;
        console.log(`[Taken] ${candidate.name} (${candidate.genre}) [Unique Memory: ${seenUsernames.size}]`);
        STATS.currentDelay = CONFIG.baseDelayMs;
      } else if (status === 'ratelimit') {
        console.warn("⚠️ Rate limited. Pausing 15s...");
        STATS.currentDelay = 15000;
      } else if (status === 'error') {
        STATS.currentDelay = 5000;
      }
    } catch (err) {
      STATS.currentDelay = 10000;
    }

    await new Promise(r => setTimeout(r, STATS.currentDelay));
  }
}

startScanner();
