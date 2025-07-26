# Portfolio Gallery Scheduler

Supabase 무료 플랜의 비활성 프로젝트 일시정지를 방지하기 위한 GitHub Actions 스케줄러입니다.

## 개요

이 프로젝트는 매주 일요일과 수요일에 [portfolio-gallery](https://portfolio-gallery-delta.vercel.app/) 페이지를 자동으로 방문하여 Supabase 데이터베이스의 활성 상태를 유지합니다. Supabase 무료 플랜은 7일간 활동이 없으면 프로젝트가 일시정지되는데, 이를 방지하기 위한 목적으로 제작되었습니다.

## 작동 방식

두 개의 스케줄러가 주 2회 실행됩니다:

### 1. Ping Homepage (수요일)
- **스케줄**: 매주 수요일 00:00 UTC
- **대상**: https://portfolio-gallery-delta.vercel.app/
- **동작**: 메인 페이지에 HTTP 요청

### 2. Ping Gallery Salon (일요일)  
- **스케줄**: 매주 일요일 00:00 UTC
- **대상**: https://portfolio-gallery-delta.vercel.app/gallery/salon
- **동작**: 갤러리 살롱 페이지에 HTTP 요청

**결과**: 정기적인 웹사이트 방문으로 Supabase 데이터베이스 연결 활동을 유지하여 프로젝트 활성 상태 보장

## 파일 구조

```
.github/
  workflows/
    ping-home.yml      # 메인 페이지 핑 (수요일)
    ping-gallery.yml   # 갤러리 살롱 페이지 핑 (일요일)
```

## 설정

GitHub Actions는 자동으로 실행되며 별도의 설정이 필요하지 않습니다. 저장소가 공개되어 있거나 GitHub Actions가 활성화된 상태에서 자동으로 작동합니다.

## 라이센스

MIT License