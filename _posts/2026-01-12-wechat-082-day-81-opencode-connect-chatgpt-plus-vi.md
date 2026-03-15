---
layout: post
title: "Day 81: opencode connect ChatGPT Plus 编写 vi 编辑器"
author: iosdevlog
date: 2026-01-12 23:59:13 +0800
description: "AI开发日志公众号专辑同步"
category: AI
tags: [AI, WeChat, BuildYourOwnXWithAI]
---

> 来源：AI开发日志公众号专辑「Build Your Own X With AI」  
> 原文链接：https://mp.weixin.qq.com/s?__biz=MzUxMjg3MjE2OA==&mid=2247486441&idx=1&sn=80fdee46e4c0d6f68e545319131f5d7a&chksm=f95c906ece2b1978037bc9558064b99468a9b6a74525244386070a7ca3d7c10198b22b3fe24f#rd

编写一个类似 vi 的命令行工具

# Questions

你希望这个类似 vi 的命令行工具用哪种语言实现？

Rust (Recommended)

目标功能范围？

最小可用

是否需要支持跨平台构建与发布？

是

# Todos

[•]

Define MVP vi-like feature set

[ ]

Design CLI UX and keybindings

[ ]

Outline Rust crate structure

[ ]

Plan core editor loop modules

[ ]

Plan cross-platform build/release

我已基于你的选择开始拟定计划：Rust + 最小可用 + 跨平台。下面是执行前的方案概览与需要你确认的细节。

方案概览

- MVP 功能：打开文件、插入文本、保存、退出

- 交互模型：简化版 vi（普通模式/插入模式/命令行模式）

- 跨平台：macOS/Linux/Windows 基础支持

- 技术栈：Rust + 终端 UI（例如 crossterm 或 ratatui）

需要你确认

- 是否要求支持多文件/缓冲区？（默认不支持）

- 是否需要方向键/鼠标支持，还是只支持 h/j/k/l？

- 保存时是否需要自动创建不存在的文件？

确认后我会进入实现阶段并写代码。

▣  Plan · gpt-5.2-codex · 39.3s

不支持;只支持 h/j/k/l; 否需要自动创建不存在的文件

收到：不支持多文件；只用 h/j/k/l；保存时不自动创建新文件。

实施计划（仅读阶段）

1. 明确 MVP 功能与模式（普通/插入/命令行）

2. 设计键位与命令（i 进入插入、Esc 退出、:w 保存、:q 退出）

3. 规划 Rust 项目结构与模块边界

4. 规划事件循环与渲染流程（基于终端库）

5. 规划跨平台构建与发布流程

确认后我进入实现阶段并开始写代码。你希望项目名是什么？

▣  Plan · gpt-5.2-codex · 7.7s

my_vi

好，项目名 my_vi。我保持只读并给出实现计划，确认后再开始写代码。

计划

- 确认 MVP 功能与模式：普通/插入/命令行，单文件编辑

- 设计键位：h/j/k/l 移动，i 进入插入，Esc 退出插入，: 进入命令行，w 保存，q 退出

- 规划 Rust 结构：main.rs 启动；editor, buffer, terminal, input, command 模块

- 设计事件循环：读取按键 → 更新状态 → 渲染

- 选择终端库并规划跨平台构建：优先 crossterm + ratatui 或纯 crossterm

需要我开始实现吗？如果有偏好：crossterm 单独使用，还是配 ratatui？

▣  Plan · gpt-5.2-codex · 8.7s

crossterm

好的，使用 crossterm。我会保持只读，先给出可执行的实现计划，确认后再进入编码阶段。

实现计划（只读规划）

- 定义编辑器状态机与模式：Normal / Insert / Command

- 设计数据结构：Buffer（行数组、光标）、Editor（模式、文件路径、dirty 标记）

- 键位映射：

- Normal：h/j/k/l 移动，i 进插入，: 进命令行，q 尝试退出

- Insert：字符插入、Backspace 删除、Enter 换行、Esc 返回 Normal

- Command：输入命令字符串，Enter 执行（:w / :q / :wq），Esc 取消

- 终端渲染流程（crossterm）：

- 进入 raw 模式、隐藏光标

- 每帧清屏 → 绘制文本区 → 绘制状态栏/命令行

- 更新光标位置并显示

- 文件读写：

- 启动时可选参数打开文件（若不存在提示错误，不自动创建）

- :w 保存仅在有路径且文件存在时写入，否则报错

- 跨平台：

- 使用 crossterm 处理输入与渲染

- 提供 cargo build --release，说明 macOS/Linux/Windows 通用构建方式

需要你确认

- 是否需要最简单的状态栏（显示模式、文件名、dirty 标记）？

- 保存策略：若文件不存在，是否直接报错并提示使用 :w filename？（默认不支持）

确认后我进入编码实现。

▣  Plan · gpt-5.2-codex · 10.8s

需要最简单的状态栏; 若文件不存在, 创建文件

确认：需要最简单状态栏；若文件不存在则创建并保存。已记录。

我将保持只读，给出最终实现计划，确认后再进入编码阶段。

实施计划

- 定义编辑器状态机与模式：Normal/Insert/Command，单文件编辑。

- 设计数据结构：Buffer（行数组、光标）、Editor（模式、文件路径、dirty）。

- 键位与命令：

- Normal：h/j/k/l 移动，i 进插入，: 进命令行。

- Insert：输入字符、Backspace 删除、Enter 换行、Esc 返回 Normal。

- Command：:w 保存（若不存在则创建），:q 退出（若 dirty 则提示），:wq 保存并退出。

- 终端渲染（crossterm）：

- raw 模式、隐藏光标；每帧清屏→文本区→状态栏→命令行。

- 状态栏显示模式/文件名/dirty 标记。

- 文件读写：

- 启动时可选参数打开文件；若不存在，显示新文件状态，:w 创建。

- 跨平台构建：

- 提供 cargo build --release 与基础说明。

如果确认无误，我就开始实现。请回复“开始实现”。

▣  Plan · gpt-5.2-codex · 7.6s

开始实现

✱ Glob "**/AGENTS.md" in .

# Lists files in repo root

$ ls

现在仍处于“只读/计划模式”，我不能做任何修改或创建文件。仓库当前看起来是空的，没有 AGENTS.md 约束。

在进入编码前，我需要你确认以下几点：

需要你确认

- 是否在当前目录初始化一个新的 Rust 项目（cargo init --bin）？

- 二进制名是否就是 my_vi？

- 是否允许我切换到可写模式并开始实现？

实施计划（可执行）

- 初始化 Rust 项目结构与依赖（crossterm）。

- 实现核心模块：buffer, editor, terminal, input, command。

- 构建事件循环：读取按键 → 更新状态 → 渲染。

- 完成模式与键位：Normal/Insert/Command + h/j/k/l、i、:、Esc、:w/:q/:wq。

- 渲染文本区与状态栏，支持文件创建保存。

- 提供跨平台构建说明（cargo build --release）。

确认上述问题后，我将开始实现。

▣  Plan · gpt-5.2-codex · 17.4s

在当前目录初始化一个新的 Rust 项目（cargo init --bin）； 二进制名就是 my_vi；允许切换到可写模式并开始实现

收到。我仍处于只读计划模式，暂不能执行 cargo init 或写文件。下面给出可直接执行的实现计划；你确认后我再开始动手。

可执行实现计划

- 初始化项目：cargo init --bin，并设置包名与二进制为 my_vi

- 添加依赖：crossterm

- 设计结构：src/main.rs 驱动；editor, buffer, terminal, input, command 模块

- 实现事件循环：读键 → 更新状态 → 渲染

- 模式与键位：Normal/Insert/Command，h/j/k/l、i、:、Esc、:w/:q/:wq

- 文件读写：启动可选打开文件；若不存在则新建标记；:w 创建并保存

- 渲染：文本区 + 最简状态栏（模式/文件名/dirty）

请回复“开始写入”，我将切换到可写模式并执行。

▣  Plan · gpt-5.2-codex · 5.6s

开始写入

当前仍处于 Plan Mode（只读），系统明确禁止任何写入/初始化操作，所以我现在不能执行 cargo init 或创建文件。

请你切换到可写模式（退出 Plan Mode），或明确授权我进入实现阶段。我确认后立刻开始初始化并写代码。

▣  Plan · gpt-5.2-codex · 3.9s

开始写入

Bad Request: bad request: Personal Access Tokens are not supported for this endpoint

开始写入

# Lists files in repo root

$ ls

# Initializes a Rust binary project

$ cargo init --bin --name my_vi

Creating binary (application) package

note: see more `Cargo.toml` keys and their definitions at https://doc.rust-lang.org/cargo/reference/manifest.html

→ Read Cargo.toml

← Edit Cargo.toml

version = "0.1.0"

edition = "2024"

[dependencies]

→ Read src/main.rs

# Wrote src/buffer.rs

use std::fs;

use std::io;

use std::path::Path;

pub struct Buffer {

lines: Vec<String>,

pub cursor_row: usize,

pub cursor_col: usize,

}

impl Buffer {

pub fn new() -> Self {

Self {

lines: vec![String::new()],

cursor_row: 0,

cursor_col: 0,

}

}

pub fn from_path(path: &Path) -> io::Result<Self> {

let content = fs::read_to_string(path)?;

let mut lines: Vec<String> = content.split('\n').map(|line| line.to_string()).collect();

if lines.is_empty() {

lines.push(String::new());

}

Ok(Self {

lines,

cursor_row: 0,

cursor_col: 0,

})

}

pub fn line_count(&self) -> usize {

self.lines.len()

}

pub fn line(&self, index: usize) -> &str {

self.lines.get(index).map(String::as_str).unwrap_or("")

}

pub fn line_len(&self, index: usize) -> usize {

self.line(index).chars().count()

}

pub fn insert_char(&mut self, ch: char) {

let line = &mut self.lines[self.cursor_row];

let byte_index = char_to_byte_index(line, self.cursor_col);

line.insert(byte_index, ch);

self.cursor_col += 1;

}

pub fn insert_newline(&mut self) {

let line = self.lines[self.cursor_row].clone();

let byte_index = char_to_byte_index(&line, self.cursor_col);

let left = line[..byte_index].to_string();

let right = line[byte_index..].to_string();

self.lines[self.cursor_row] = left;

self.lines.insert(self.cursor_row + 1, right);

self.cursor_row += 1;

self.cursor_col = 0;

}

pub fn delete_back(&mut self) {

if self.cursor_col > 0 {

let line = &mut self.lines[self.cursor_row];

let byte_index = char_to_byte_index(line, self.cursor_col - 1);

line.remove(byte_index);

self.cursor_col -= 1;

return;

}

if self.cursor_row == 0 {

return;

}

let current = self.lines.remove(self.cursor_row);

self.cursor_row -= 1;

let line = &mut self.lines[self.cursor_row];

let previous_len = line.chars().count();

line.push_str(&current);

self.cursor_col = previous_len;

}

pub fn move_left(&mut self) {

if self.cursor_col > 0 {

self.cursor_col -= 1;

} else if self.cursor_row > 0 {

self.cursor_row -= 1;

self.cursor_col = self.line_len(self.cursor_row);

}

}

pub fn move_right(&mut self) {

let line_len = self.line_len(self.cursor_row);

if self.cursor_col < line_len {

self.cursor_col += 1;

} else if self.cursor_row + 1 < self.lines.len() {

self.cursor_row += 1;

self.cursor_col = 0;

}

}

pub fn move_up(&mut self) {

if self.cursor_row > 0 {

self.cursor_row -= 1;

let line_len = self.line_len(self.cursor_row);

if self.cursor_col > line_len {

self.cursor_col = line_len;

}

}

}

pub fn move_down(&mut self) {

if self.cursor_row + 1 < self.lines.len() {

self.cursor_row += 1;

let line_len = self.line_len(self.cursor_row);

if self.cursor_col > line_len {

self.cursor_col = line_len;

}

}

}

pub fn to_string(&self) -> String {

self.lines.join("\n")

}

}

fn char_to_byte_index(line: &str, char_index: usize) -> usize {

if char_index == 0 {

return 0;

}

let mut count = 0;

for (byte_index, _) in line.char_indices() {

if count == char_index {

return byte_index;

}

count += 1;

}

line.len()

}

# Wrote src/editor.rs

use crate::buffer::Buffer;

use crossterm::cursor::MoveTo;

use crossterm::event::{self, Event, KeyCode, KeyEvent, KeyModifiers};

use crossterm::style::{Attribute, Print, SetAttribute};

use crossterm::terminal::{self, Clear, ClearType};

use crossterm::{queue, Result};

use std::cmp::{min, Ordering};

use std::io::{self, Write};

use std::path::{Path, PathBuf};

pub enum Mode {

Normal,

Insert,

Command,

}

pub struct Editor {

buffer: Buffer,

mode: Mode,

command_input: String,

message: Option<String>,

file_path: Option<PathBuf>,

dirty: bool,

scroll_offset: usize,

should_quit: bool,

}

impl Editor {

pub fn new(buffer: Buffer, file_path: Option<PathBuf>) -> Self {

Self {

buffer,

mode: Mode::Normal,

command_input: String::new(),

message: None,

file_path,

dirty: false,

scroll_offset: 0,

should_quit: false,

}

}

pub fn run(&mut self) -> Result<()> {

loop {

self.render()?;

if self.should_quit {

break;

}

if let Event::Key(key_event) = event::read()? {

self.handle_key(key_event);

}

}

Ok(())

}

fn handle_key(&mut self, key_event: KeyEvent) {

match self.mode {

Mode::Normal => self.handle_normal_mode(key_event),

Mode::Insert => self.handle_insert_mode(key_event),

Mode::Command => self.handle_command_mode(key_event),

}

}

fn handle_normal_mode(&mut self, key_event: KeyEvent) {

match key_event.code {

KeyCode::Char('h') => self.buffer.move_left(),

KeyCode::Char('j') => self.buffer.move_down(),

KeyCode::Char('k') => self.buffer.move_up(),

KeyCode::Char('l') => self.buffer.move_right(),

KeyCode::Char('i') => self.mode = Mode::Insert,

KeyCode::Char(':') => {

self.mode = Mode::Command;

self.command_input.clear();

}

KeyCode::Char('q') => {

self.message = Some("Use :q to quit".to_string());

}

_ => {}

}

}

fn handle_insert_mode(&mut self, key_event: KeyEvent) {

match key_event.code {

KeyCode::Esc => self.mode = Mode::Normal,

KeyCode::Enter => {

self.buffer.insert_newline();

self.dirty = true;

}

KeyCode::Backspace => {

self.buffer.delete_back();

self.dirty = true;

}

KeyCode::Char(ch) => {

if !key_event.modifiers.contains(KeyModifiers::CONTROL) {

self.buffer.insert_char(ch);

self.dirty = true;

}

}

_ => {}

}

}

fn handle_command_mode(&mut self, key_event: KeyEvent) {

match key_event.code {

KeyCode::Esc => {

self.mode = Mode::Normal;

self.command_input.clear();

}

KeyCode::Enter => {

let command = self.command_input.trim().to_string();

self.mode = Mode::Normal;

self.command_input.clear();

self.execute_command(command);

}

KeyCode::Backspace => {

self.command_input.pop();

}

KeyCode::Char(ch) => {

if !key_event.modifiers.contains(KeyModifiers::CONTROL) {

self.command_input.push(ch);

}

}

_ => {}

}

}

fn execute_command(&mut self, command: String) {

if command.is_empty() {

return;

}

let mut parts = command.split_whitespace();

match parts.next() {

Some("w") => {

if let Some(path) = parts.next() {

self.file_path = Some(PathBuf::from(path));

}

if let Some(path) = self.file_path.clone() {

self.save_to_path(&path);

} else {

self.message = Some("No file name".to_string());

}

}

Some("q") => {

if self.dirty {

self.message = Some("Unsaved changes".to_string());

} else {

self.should_quit = true;

}

}

Some("q!") => {

self.should_quit = true;

}

Some("wq") => {

if let Some(path) = self.file_path.clone() {

if self.save_to_path(&path) {

self.should_quit = true;

}

} else {

self.message = Some("No file name".to_string());

}

}

_ => {

self.message = Some(format!("Unknown command: {}", command));

}

}

}

fn save_to_path(&mut self, path: &Path) -> bool {

match std::fs::write(path, self.buffer.to_string()) {

Ok(()) => {

self.dirty = false;

self.message = Some("Written".to_string());

true

}

Err(err) => {

self.message = Some(format!("Write error: {}", err));

false

}

}

}

fn render(&mut self) -> Result<()> {

let (cols, rows) = terminal::size()?;

let mut stdout = io::stdout();

let usable_rows = rows.saturating_sub(2) as usize;

self.ensure_cursor_visible(usable_rows);

for row in 0..usable_rows {

let line_index = self.scroll_offset + row;

let line = if line_index < self.buffer.line_count() {

self.buffer.line(line_index)

} else {

"~"

};

let content = trim_to_width(line, cols as usize);

queue!(stdout, MoveTo(0, row as u16), Clear(ClearType::CurrentLine), Print(content))?;

}

let status_line = self.build_status_line(cols as usize);

let status_row = rows.saturating_sub(2);

queue!(

stdout,

MoveTo(0, status_row),

SetAttribute(Attribute::Reverse),

Clear(ClearType::CurrentLine),

Print(status_line),

SetAttribute(Attribute::Reset)

)?;

let command_row = rows.saturating_sub(1);

let command_text = if matches!(self.mode, Mode::Command) {

format!(":{}", self.command_input)

} else {

self.message.clone().unwrap_or_default()

};

let command_line = trim_to_width(&command_text, cols as usize);

queue!(

stdout,

MoveTo(0, command_row),

Clear(ClearType::CurrentLine),

Print(command_line)

)?;

let cursor_row = self.buffer.cursor_row.saturating_sub(self.scroll_offset);

let cursor_col = min(self.buffer.cursor_col, cols as usize.saturating_sub(1));

match cursor_row.cmp(&usable_rows) {

Ordering::Less => {

queue!(stdout, MoveTo(cursor_col as u16, cursor_row as u16))?;

}

_ => {

queue!(stdout, MoveTo(0, status_row))?;

}

}

stdout.flush()?;

Ok(())

}

fn ensure_cursor_visible(&mut self, usable_rows: usize) {

if usable_rows == 0 {

return;

}

if self.buffer.cursor_row < self.scroll_offset {

self.scroll_offset = self.buffer.cursor_row;

} else if self.buffer.cursor_row >= self.scroll_offset + usable_rows {

self.scroll_offset = self.buffer.cursor_row + 1 - usable_rows;

}

}

fn build_status_line(&self, width: usize) -> String {

let mode = match self.mode {

Mode::Normal => "NORMAL",

Mode::Insert => "INSERT",

Mode::Command => "COMMAND",

};

let file_name = self

.file_path

.as_ref()

.and_then(|path| path.file_name())

.and_then(|name| name.to_str())

.unwrap_or("[No Name]");

let dirty = if self.dirty { " +" } else { "" };

let row = self.buffer.cursor_row + 1;

let col = self.buffer.cursor_col + 1;

let status = format!("{} | {}{} | {}:{}", mode, file_name, dirty, row, col);

pad_to_width(&status, width)

}

}

fn trim_to_width(input: &str, width: usize) -> String {

input.chars().take(width).collect()

}

fn pad_to_width(input: &str, width: usize) -> String {

let mut result = trim_to_width(input, width);

let len = result.chars().count();

if len < width {

result.push_str(&" ".repeat(width - len));

}

result

}

# Wrote src/terminal.rs

use crossterm::cursor::{Hide, Show};

use crossterm::terminal::{disable_raw_mode, enable_raw_mode, EnterAlternateScreen, LeaveAlternateScreen};

use crossterm::{execute, Result};

use std::io::stdout;

pub struct TerminalGuard;

impl TerminalGuard {

pub fn new() -> Result<Self> {

enable_raw_mode()?;

execute!(stdout(), EnterAlternateScreen, Hide)?;

Ok(Self)

}

}

impl Drop for TerminalGuard {

fn drop(&mut self) {

let _ = disable_raw_mode();

let _ = execute!(stdout(), Show, LeaveAlternateScreen);

}

}

# Wrote src/main.rs

mod buffer;

mod editor;

mod terminal;

use buffer::Buffer;

use editor::Editor;

use std::env;

use std::path::PathBuf;

use terminal::TerminalGuard;

fn main() -> Result<(), Box<dyn std::error::Error>> {

let file_path = env::args().nth(1).map(PathBuf::from);

let (buffer, file_path) = if let Some(path) = file_path {

match Buffer::from_path(&path) {

Ok(buffer) => (buffer, Some(path)),

Err(err) if err.kind() == std::io::ErrorKind::NotFound => (Buffer::new(), Some(path)),

Err(err) => return Err(err.into()),

}

} else {

(Buffer::new(), None)

};

let _terminal = TerminalGuard::new()?;

let mut editor = Editor::new(buffer, file_path);

editor.run()?;

Ok(())

}

# Runs Rust cargo check

$ cargo check

Updating crates.io index

Locking 32 packages to latest Rust 1.91.1 compatible versions

Adding crossterm v0.27.0 (available: v0.29.0)

Downloading crates ...

Downloaded errno v0.3.14

Downloaded crossterm v0.27.0

Downloaded signal-hook-mio v0.2.5

Downloaded signal-hook-registry v1.4.8

Downloaded mio v0.8.11

Downloaded signal-hook v0.3.18

…

Click to expand

← Edit src/editor.rs

use crossterm::cursor::MoveTo;

use crossterm::event::{self, Event, KeyCode, KeyEvent, KeyModifiers};

use crossterm::style::{Attribute, Print, SetAttribute};

use crossterm::terminal::{self, Clear, ClearType};

use crossterm::{queue, Result};

use std::cmp::{min, Ordering};

use std::io::{self, Write};

use std::path::{Path, PathBuf};

← Edit src/editor.rs

should_quit: false,

}

}

pub fn run(&mut self) -> Result<()> {

loop {

self.render()?;

if self.should_quit {

break;

← Edit src/editor.rs

}

}

}

fn render(&mut self) -> Result<()> {

let (cols, rows) = terminal::size()?;

let mut stdout = io::stdout();

let usable_rows = rows.saturating_sub(2) as usize;

self.ensure_cursor_visible(usable_rows);

← Edit src/editor.rs

Print(command_line)

)?;

let cursor_row = self.buffer.cursor_row.saturating_sub(self.scroll_offset);

let cursor_col = min(self.buffer.cursor_col, cols as usize.saturating_sub(1));

match cursor_row.cmp(&usable_rows) {

Ordering::Less => {

queue!(stdout, MoveTo(cursor_col as u16, cursor_row as u16))?;

}

← Edit src/terminal.rs

use crossterm::cursor::{Hide, Show};

use crossterm::terminal::{disable_raw_mode, enable_raw_mode, EnterAlternateScreen, LeaveAlternateScreen};

use crossterm::{execute, Result};

use std::io::stdout;

pub struct TerminalGuard;

impl TerminalGuard {

← Edit src/terminal.rs

pub struct TerminalGuard;

impl TerminalGuard {

pub fn new() -> Result<Self> {

enable_raw_mode()?;

execute!(stdout(), EnterAlternateScreen, Hide)?;

Ok(Self)

}

# Runs Rust cargo check

$ cargo check

Checking my_vi v0.1.0 (/Users/i/Code/Build_Your_Onw_X_With_AI/my_vi)

Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.09s

# Todos

[✓]

Define MVP vi-like feature set

[✓]

Design CLI UX and keybindings

[✓]

Outline Rust crate structure

[✓]

Plan core editor loop modules

[✓]

Plan cross-platform build/release

→ Read src/main.rs

→ Read src/editor.rs

→ Read src/buffer.rs

→ Read src/terminal.rs

→ Read Cargo.toml

Summary

- Initialized a Rust my_vi binary with crossterm and a minimal vi-like editor loop, modes, command handling, rendering, and status line in src/main.rs and supporting modules src/editor.rs, src/buffer.rs, src/terminal.rs. (src/main.rs:1, src/editor.rs:1, src/buffer.rs:1, src/terminal.rs:1)

- Added crossterm dependency in Cargo.toml. (Cargo.toml:1)

Usage

- Build/run: cargo run -- [path]

- Normal mode: h/j/k/l move, i insert, : command

- Insert mode: type to insert, Backspace, Enter, Esc to normal

- Command mode: :w save (creates file if missing), :q quit, :wq save+quit, :q! force quit

Tests

- cargo check

Want me to add basic :w filename support to set a new file name (it already works), or keep it minimal as-is?

▣  Build · gpt-5.2-codex · 3m 58s

添加 README，有中英文 2 个版本

# Wrote README.md

# my_vi

A minimal vi-like terminal editor written in Rust with `crossterm`.

## Features

- Normal/Insert/Command modes

- `h/j/k/l` movement

- Basic editing (insert, backspace, newline)

- Command mode: `:w`, `:q`, `:wq`, `:q!`

- Status line showing mode, filename, and cursor position

## Build

```bash

cargo build --release

```

## Run

```bash

cargo run -- [path]

```

- When `path` does not exist, it is created on `:w`.

## Keybindings

### Normal mode

- `h/j/k/l`: move cursor

- `i`: enter insert mode

- `:`: enter command mode

### Insert mode

- Type to insert

- `Backspace`: delete

- `Enter`: newline

- `Esc`: back to normal mode

### Command mode

- `:w` save

- `:q` quit (blocked if unsaved)

- `:q!` quit without saving

- `:wq` save and quit

# Wrote README_CN.md

# my_vi

一个使用 Rust 与 `crossterm` 编写的最小化类 vi 终端编辑器。

## 功能

- 普通/插入/命令三种模式

- `h/j/k/l` 光标移动

- 基础编辑（插入、退格、换行）

- 命令模式：`:w`、`:q`、`:wq`、`:q!`

- 状态栏显示模式、文件名与光标位置

## 构建

```bash

cargo build --release

```

## 运行

```bash

cargo run -- [path]

```

- 当 `path` 不存在时，会在 `:w` 保存时创建。

## 键位

### 普通模式

- `h/j/k/l`：移动光标

- `i`：进入插入模式

- `:`：进入命令模式

### 插入模式

- 直接输入字符

- `Backspace`：删除

- `Enter`：换行

- `Esc`：返回普通模式

### 命令模式

- `:w` 保存

- `:q` 退出（有未保存时提示）

- `:q!` 强制退出不保存

- `:wq` 保存并退出

Summary

- Added English README at README.md:1.

- Added Chinese README at README_CN.md:1.

Anything else you want documented (e.g., screenshots, roadmap, or build badges)?

▣  Build · gpt-5.2-codex · 20.9s

提交 Git

# Shows working tree status

$ git status -sb

# New session - 2026-01-12T15:30:04.978Z

## No commits yet on main

?? .gitignore

?? Cargo.lock

?? Cargo.toml

?? README.md

?? README_CN.md

?? src/

# Shows working tree diff

$ git diff

# Shows recent commits

$ git log -5 --oneline

fatal: your current branch 'main' does not have any commits yet

# Stages files, commits, and shows status

$ git add . && git commit -m "Add minimal vi-like editor and docs" && git status -sb

[main (root-commit) e73fabe] Add minimal vi-like editor and docs

9 files changed, 850 insertions(+)

create mode 100644 .gitignore

create mode 100644 Cargo.lock

create mode 100644 Cargo.toml

create mode 100644 README.md

create mode 100644 README_CN.md

create mode 100644 src/buffer.rs

create mode 100644 src/editor.rs

create mode 100644 src/main.rs

…

Click to expand

Commit created successfully.

Commit

- e73fabe Add minimal vi-like editor and docs

Anything else you want me to do (e.g., tag a release or push)?

/init

create/update AGENTS.md

/review

review changes [commit|branch|pr], defaults to uncommitted

/undo

undo the last message

/redo

redo the last message

/compact

compact the session

/rename

▣  Build · gpt-5.2-codex · 16.3s

rename session

/copy

copy session transcript to clipboard

Build

GPT-5.2 Codex

OpenAI

my_vi

一个使用 Rust 与 crossterm 编写的最小化类 vi 终端编辑器。

功能

普通/插入/命令三种模式

h/j/k/l

光标移动

基础编辑（插入、退格、换行）

命令模式：:w、:q、:wq、:q!

状态栏显示模式、文件名与光标位置

构建

cargo build --release

运行

cargo run -- [path]

当 path 不存在时，会在 :w 保存时创建。

键位

普通模式

h/j/k/l

：移动光标

i

：进入插入模式

:

：进入命令模式

插入模式

直接输入字符

Backspace

：删除

Enter

：换行

Esc

：返回普通模式

命令模式

:w

保存

:q

退出（有未保存时提示）

:q!

强制退出不保存

:wq

保存并退出

![image-1](https://mmbiz.qpic.cn/sz_mmbiz_png/kIE7WtwNFTRB1juo4ogW3SeXR037d6OOwkFePdbbzEfLgz0AOWFzQPFX5NPYFtTYm9ciaYicsDFkm3D8qAWpSS2A/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=0)
