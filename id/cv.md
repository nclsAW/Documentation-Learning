# CV

## Context & Business Goal

***

Pembuatan CV secara otomatis menggunakan template yang telah disiapkan, dibuat untuk memberikan kemudahan dalam membuat CV berulang yang memerlukan pergantian data secara teratur. Program ini ditujukan untuk diri sendiri.

## Architecture & High-Level Flow

***

### Flowchart

### Tech Stack

| Module   | **Stack**      |
| -------- | -------------- |
| Frontend | Nuxt.js        |
| Backend  | NestJS, Prisma |
| Database | PostgreSQL     |

## Structures

***

### Frontend

* components
  * experience
  * skill
  * settings
* layouts
* pages
  * create
  * experiences
  * generator
  * profile
  * settings
  * skill
* stores

### Backend

* src
  * data
    * dto
    * \*controller.ts
    * \*service.ts
    * \*module.ts
* prisma

## Core Data Model

***

### Database Schema/ERD

### REST API

GET

/data/full-profile

200 OK

```
{
  "personalInfos": [
    {
      "id": "clx123personal001",
      "fullName": "Example",
      "email": "example@example.com",
      "phone": "081234567890",
      "address": "Jakarta, Indonesia",
      "summary": "IT Example",
      "photoUrl": "http://localhost:3001/uploads/profile.jpg",
      "createdAt": "2026-10-20T10:00:00.000Z",
      "updatedAt": "2026-10-20T10:00:00.000Z"
    }
  ],
  "experiences": [
    {
      "id": "clx123exp001",
      "title": "Software QA & Compliance",
      "company": "Example Corp",
      "location": "Jakarta, Indonesia",
      "startDate": "2024-05-01T00:00:00.000Z",
      "endDate": null,
      "isCurrent": true,
      "description": "Authoring test scenarios, defect reports, and running automated Playwright integration tests."
    }
  ],
  "education": [
    {
      "id": "clx123edu001",
      "institution": "Example University",
      "degree": "Bachelor of Computer Science",
      "fieldOfStudy": "Informatics",
      "startDate": "2020-09-01T00:00:00.000Z",
      "endDate": "2024-08-31T00:00:00.000Z",
      "grade": "3.85",
      "description": "Focused on Software Engineering, Database Systems, and Architecture."
    }
  ],
  "projects": [
    {
      "id": "clx123proj001",
      "title": "JobTracks Workspace",
      "description": "Fullstack job application tracker built with NestJS, Prisma, PostgreSQL, and Vue 3.",
      "techStack": ["NestJS", "Vue 3", "Prisma", "PostgreSQL", "Tailwind CSS"],
      "repoUrl": "https://github.com/example/jobtracks",
      "demoUrl": "https://jobtracks.example.com"
    }
  ],
  "skills": [
    {
      "id": "clx123skill001",
      "name": "Vue.js 3",
      "category": "Frontend Engineering",
      "level": "Advanced"
    }
  ],
  "achievements": [
    {
      "id": "clx123ach001",
      "title": "Example Certification",
      "issuer": "Example",
      "date": "2026-01-15T00:00:00.000Z",
      "credentialUrl": "https://credentials.example.com/cert/123"
    }
  ]
}
```

POST

/data/restore

```
{
  "personalInfos": [
    {
      "fullName": "Example",
      "email": "example@example.com",
      "phone": "081234567890",
      "address": "Jakarta, Indonesia",
      "summary": "IT Example"
    }
  ],
  "experiences": [
    {
      "title": "Software QA",
      "company": "Logistics Tech",
      "startDate": "2024-05-01",
      "endDate": ""
    }
  ],
  "education": [
    {
      "institution": "Example University",
      "degree": "Bachelor of Computer Science",
      "fieldOfStudy": "Informatics",
      "startDate": "2020-09-01",
      "endDate": "2024-08-31"
    }
  ],
  "projects": [],
  "skills": [],
  "achievements": []
}
```

201 Created

```
{
  "success": true
}
```

/data/personal-info

Request Body application/json

```
{
  "fullName": "Example",
  "email": "example@example.com",
  "phone": "081234567890",
  "address": "Jakarta, Indonesia",
  "summary": "IT Example"
}
```

201 Created

```
{
  "id": "clx123personal001",
  "fullName": "Nicolas Anelka Winata",
  "email": "nicolas@example.com",
  "phone": "081234567890",
  "address": "Jakarta, Indonesia",
  "summary": "IT Logistics & Compliance Specialist with expertise in NestJS, Vue 3, and Automated Testing.",
  "photoUrl": null,
  "createdAt": "2026-10-20T10:00:00.000Z",
  "updatedAt": "2026-10-20T10:00:00.000Z"
}
```

/data/experience

Request Body application/json:

```
{
  "title": "Software Quality Assurance",
  "company": "Example Company",
  "location": "Jakarta, Indonesia",
  "startDate": "2024-05-01",
  "endDate": "",
  "isCurrent": true,
  "description": "Responsible for API automation testing, end-to-end regression testing using Playwright, and managing Jira defect logs."
}
```

Response 201 Created:

```
{
  "id": "clx123exp001",
  "title": "Software Quality Assurance",
  "company": "Logistics Tech Corp",
  "location": "Jakarta, Indonesia",
  "startDate": "2024-05-01T00:00:00.000Z",
  "endDate": null,
  "isCurrent": true,
  "description": "Responsible for API automation testing, end-to-end regression testing using Playwright, and managing Jira defect logs.",
  "createdAt": "2026-10-20T10:00:00.000Z"
}
```

/data/education

Request Body application/json:

```
{
  "institution": "Example University",
  "degree": "Bachelor of Computer Science",
  "fieldOfStudy": "Informatics",
  "startDate": "2020-09-01",
  "endDate": "2024-08-31",
  "grade": "3.85",
  "description": "Studied Software Engineering, Database Design, and Web Systems."

}
```

Response 201 Created:

```
{
  "id": "clx123edu001",
  "institution": "Example University",
  "degree": "Bachelor of Computer Science",
  "fieldOfStudy": "Informatics",
  "startDate": "2020-09-01T00:00:00.000Z",
  "endDate": "2024-08-31T00:00:00.000Z",
  "grade": "3.85",
  "description": "Studied Software Engineering, Database Design, and Web Systems."
}
```

/data/skill

Request Body application/json:

```
{
  "name": "NestJS",
  "category": "Backend Development",
  "level": "Advanced"
}
```

Response 201 Created:

```
{
  "id": "clx123skill001",
  "name": "NestJS",
  "category": "Backend Development",
  "level": "Advanced"
}
```

/data/project

Request Body application/json:

```
{
  "title": "HubEngine Workspace",
  "description": "Multi-schema dynamic data workspace featuring PostgreSQL JSONB records and dynamic node visual flowcharts.",
  "techStack": ["NestJS", "Vue 3", "Prisma", "PostgreSQL", "Tailwind CSS"],
  "repoUrl": "https://github.com/example/hubengine",
  "demoUrl": "https://hubengine.example.com"
}
```

Response 201 Created:

```
{
  "id": "clx123proj001",
  "title": "HubEngine Workspace",
  "description": "Multi-schema dynamic data workspace featuring PostgreSQL JSONB records and dynamic node visual flowcharts.",
  "techStack": ["NestJS", "Vue 3", "Prisma", "PostgreSQL", "Tailwind CSS"],
  "repoUrl": "https://github.com/example/hubengine",
  "demoUrl": "https://hubengine.example.com"
}
```

/data/acihevement

Request Body application/json:

```
{
  "title": "Playwright Automation Testing Certification",
  "issuer": "Software Testing Institute",
  "date": "2026-06-10",
  "description": "Certified for building enterprise test automation frameworks.",
  "credentialUrl": "https://cert.example.com/verify/qa-456"
}
```

Response 201 Created:

```
{
  "id": "clx123ach001",
  "title": "Playwright Automation Testing Certification",
  "issuer": "Software Testing Institute",
  "date": "2026-06-10T00:00:00.000Z",
  "description": "Certified for building enterprise test automation frameworks.",
  "credentialUrl": "https://cert.example.com/verify/qa-456"
}
```

PATCH

/data/personal-info/:id

Header: Content-Type: multipart/form-data

Body Form Data:

* photo: (binary file/profile.jpg)
* fullName: “Example“
* phone: “08121234567890”

Response 200 OK:

```
{
  "id": "clx123personal001",
  "fullName": "Example",
  "email": "example@example.com",
  "phone": "081299998888",
  "address": "Jakarta, Indonesia",
  "summary": "IT Example",
  "photoUrl": "http://localhost:3001/uploads/profile.jpg",
  "updatedAt": "2026-10-20T10:05:00.000Z"
}
```

/data/experience/:id

Request Body application/json:

```
{
  "endDate": "2026-10-01",
  "isCurrent": false
}
```

Response 200 OK:

```
{
  "id": "clx123exp001",
  "title": "Software Quality Assurance",
  "company": "ExampleCorp",
  "location": "Jakarta, Indonesia",
  "startDate": "2024-05-01T00:00:00.000Z",
  "endDate": "2026-10-01T00:00:00.000Z",
  "isCurrent": false,
  "description": "Responsible for API automation testing, end-to-end regression testing using Playwright, and managing Jira defect logs."
}
```

/data/education/:id

Request Body application/json:

```
{
  "grade": "3.90"
}
```

Response 200 OK:

```
{
  "id": "clx123edu001",
  "institution": "Example University",
  "degree": "Bachelor of Computer Science",
  "fieldOfStudy": "Informatics",
  "startDate": "2020-09-01T00:00:00.000Z",
  "endDate": "2024-08-31T00:00:00.000Z",
  "grade": "3.90",
  "description": "Studied Software Engineering, Database Design, and Web Systems."
}
```

/data/skill/:id

Request Body application/json:

```
{
  "level": "Expert"
}
```

Response 200 OK:

```
{
  "id": "clx123skill001",
  "name": "NestJS",
  "category": "Backend Development",
  "level": "Expert"
}
```

/data/project/:id

Request Body application/json:

```
{
  "demoUrl": "https://v2.hubengine.example.com"
}
```

Response 200 OK:

```
{
  "id": "clx123proj001",
  "title": "HubEngine Workspace",
  "description": "Multi-schema dynamic data workspace featuring PostgreSQL JSONB records and dynamic node visual flowcharts.",
  "techStack": ["NestJS", "Vue 3", "Prisma", "PostgreSQL", "Tailwind CSS"],
  "repoUrl": "https://github.com/example/hubengine",
  "demoUrl": "https://v2.hubengine.example.com"
}
```

/data/achievement/:id

Request Body application/json:

```
{
  "title": "Advanced Playwright Automation Testing Certification"
}
```

Response 200 OK:

```
{
  "id": "clx123ach001",
  "title": "Example Testing Certification",
  "issuer": "Software Testing Example",
  "date": "2026-06-10T00:00:00.000Z",
  "description": "Certified for building enterprise test automation frameworks.",
  "credentialUrl": "https://cert.example.com/verify/qa-456"
}
```
