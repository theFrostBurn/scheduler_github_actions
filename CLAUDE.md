# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **Portfolio Gallery Scheduler** - a GitHub Actions-based project designed to prevent Supabase free tier projects from being paused due to inactivity. The project automatically pings a portfolio gallery website (https://portfolio-gallery-delta.vercel.app/) twice weekly to maintain database activity.

## Architecture

### Core Components

**GitHub Actions Workflows** (`.github/workflows/`):
- `ping-home.yml` - Pings main homepage every Wednesday at 00:00 UTC
- `ping-gallery.yml` - Pings gallery salon page every Sunday at 00:00 UTC

### Strategic Design
- **Timing**: Twice weekly schedule ensures activity within Supabase's 7-day free tier limit
- **Targets**: Different pages to simulate varied user activity
- **Method**: Simple curl requests with output redirected to /dev/null

## Key Files

### Workflow Files
- **ping-home.yml**: `cron: '0 0 * * 3'` (Wednesday)
  - Target: `https://portfolio-gallery-delta.vercel.app/`
- **ping-gallery.yml**: `cron: '0 0 * * 0'` (Sunday)  
  - Target: `https://portfolio-gallery-delta.vercel.app/gallery/salon`

### Documentation
- **README.md**: Korean documentation explaining project purpose and operation
- **CLAUDE.md**: This file

## Development Guidelines

### Modifying Schedules
- Cron format: `'minute hour day-of-month month day-of-week'`
- Ensure at least one ping every 6 days to maintain Supabase activity
- Use UTC timezone for consistency

### Adding New Endpoints
When adding new ping targets:
1. Create new workflow file in `.github/workflows/`
2. Follow naming pattern: `ping-[target].yml`
3. Update README.md to reflect new schedules
4. Ensure curl command includes error handling

### Workflow Structure Template
```yaml
name: Ping [Target Name]
on:
  schedule:
    - cron: '[schedule]'  # Comment with human-readable time
jobs:
  ping:
    runs-on: ubuntu-latest
    steps:
      - name: Ping [target description]
        run: curl -s [URL] > /dev/null
```

## Troubleshooting

### Common Issues
- **Workflow not running**: Check repository settings for Actions permissions
- **Ping failures**: Verify target URLs are accessible
- **Schedule conflicts**: Ensure cron expressions are valid

### Testing Workflows
GitHub Actions workflows can be manually triggered for testing:
1. Go to Actions tab in GitHub repository
2. Select workflow to test
3. Click "Run workflow" button

## Security Considerations

- No sensitive data is stored or transmitted
- Target URLs are public endpoints
- Actions run in isolated GitHub-hosted runners
- No authentication credentials required

## Maintenance

### Regular Tasks
- Monitor GitHub Actions execution logs
- Verify target website accessibility
- Update URLs if portfolio site moves
- Check Supabase project status periodically

### Future Enhancements
Consider adding:
- Failure notifications (GitHub Issues, email)
- Success logging to verify pings occurred
- Multiple backup URLs in case primary fails
- Health check endpoint monitoring

## 추가 규칙

1. 답변은 항상 한국어로 할 것.
2. 라이브러리 관련된 코드 생성 및 수정시에는 context7 MCP 를 항상 이용할 것.
3. DB에 관련한 코드 생성 및 수정시에는 항상 supabse MCP 와 연결해서 스키마와 정책을 확인할 것.
4. (next.js 프로젝트의 경우) 테스트가 필요하면, 스스로 npm run dev 명령어를 실행하지 말고, 사용자에게 테스트를 요청할 것.