# community-chat-forensics | Customer Chat Forensics

A Claude skill (Agent Skill) that teaches Claude to analyze customer service group chats and online support conversations with a consistent method:

- Merge scattered messages into distinct "consultation cases";
- Classify, tag, and record the status visible in the chat;
- Measure response times and broken chains, and judge whether each case was truly closed;
- Identify risks such as credential exposure, dissatisfaction signals, and handoffs that went nowhere;
- Find problem clusters that span multiple cases;
- Produce a three-layer report: case index, categories and handling, and overall findings.

Works with customer service groups on WeCom (WeChat Work), DingTalk, Feishu/Lark, Slack and similar platforms, as well as online support chat logs. Claude replies in the language you use.

## Installation

- **Claude (web or desktop)**: Zip this folder, then upload it under Settings → Skills.
- **Claude Code**: Copy this folder to `~/.claude/skills/community-chat-forensics/`.

## Usage

After installing, tell Claude:

> Use community chat forensics to analyze these chat logs

Then provide the chat records (exported files, screenshots, or pasted text). Claude will first confirm the scope, the list of speakers, and the purpose of the analysis before it begins.

## Privacy

Chat logs usually contain personal information about customers and staff. Only use this skill where you are authorized to process such data. Before sharing results externally, replace or remove customer names, personal names, account IDs, links, and personal details in screenshots. The skill instructs Claude never to transcribe account names, passwords, or authorization codes.

## License

MIT License. See [LICENSE](LICENSE).
