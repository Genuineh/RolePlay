# 项目架构文档
# Historical Deep Dive - Architecture Documentation

## 目录 / Table of Contents
1. [系统架构概览 / System Architecture Overview](#system-architecture-overview)
2. [技术选型 / Technology Stack](#technology-stack)
3. [模块设计 / Module Design](#module-design)
4. [数据流 / Data Flow](#data-flow)
5. [存储方案 / Storage Strategy](#storage-strategy)
6. [AI集成架构 / AI Integration Architecture](#ai-integration-architecture)
7. [性能优化 / Performance Optimization](#performance-optimization)
8. [安全设计 / Security Design](#security-design)

---

## System Architecture Overview

### 整体架构图

```
┌─────────────────────────────────────────────────────────────┐
│                     Presentation Layer                       │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐   │
│  │  Home    │  │  Player  │  │ Creator  │  │ Library  │   │
│  │  Screen  │  │  Screen  │  │  Screen  │  │  Screen  │   │
│  └────┬─────┘  └────┬─────┘  └────┬─────┘  └────┬─────┘   │
│       │             │              │             │          │
│       └─────────────┴──────────────┴─────────────┘          │
│                          │                                   │
│                    Riverpod Providers                        │
│                          │                                   │
└──────────────────────────┼───────────────────────────────────┘
                           │
┌──────────────────────────┼───────────────────────────────────┐
│                     Business Layer                           │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐      │
│  │   Story      │  │     User     │  │  Achievement │      │
│  │  Repository  │  │  Repository  │  │  Repository  │      │
│  └──────┬───────┘  └──────┬───────┘  └──────┬───────┘      │
│         │                 │                  │               │
│         └─────────────────┴──────────────────┘               │
│                          │                                   │
└──────────────────────────┼───────────────────────────────────┘
                           │
┌──────────────────────────┼───────────────────────────────────┐
│                      Service Layer                           │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐      │
│  │   Package    │  │   Storage    │  │      AI      │      │
│  │   Service    │  │   Service    │  │   Service    │      │
│  └──────┬───────┘  └──────┬───────┘  └──────┬───────┘      │
│         │                 │                  │               │
│    ┌────┴────┐       ┌────┴────┐       ┌────┴────┐         │
│    │ Archive │       │  Hive   │       │  HTTP   │         │
│    │file_picker│     │path_provider│   │   dio   │         │
│    └─────────┘       └─────────┘       └─────────┘         │
└──────────────────────────────────────────────────────────────┘
                           │
┌──────────────────────────┼───────────────────────────────────┐
│                      Data Layer                              │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐      │
│  │    Story     │  │     Node     │  │   Question   │      │
│  │    Model     │  │    Model     │  │    Model     │      │
│  └──────────────┘  └──────────────┘  └──────────────┘      │
│                                                              │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐      │
│  │ Achievement  │  │UserProgress  │  │    Asset     │      │
│  │    Model     │  │    Model     │  │    Model     │      │
│  └──────────────┘  └──────────────┘  └──────────────┘      │
└──────────────────────────────────────────────────────────────┘
```

For complete architecture documentation including data models, services, repositories, AI integration, and security design, please see the full ARCHITECTURE.md file.

This document provides a high-level overview of the system architecture for the Historical Deep Dive project.

**Document Version**: 1.0  
**Last Updated**: 2025-12-02  
**Maintainer**: Historical Deep Dive Team
