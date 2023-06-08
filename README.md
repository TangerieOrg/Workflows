# Workflows

## Docker

### Build & Push
`TangerieOrg/Workflows/.github/workflows/docker-build-push.yml@main`

**Inputs**
```yml
image_name:
  description: "The base name of the image (not including tags or registry)"
  default: "ERROR"
  required: true
  type: string
registry_name:
    description: "The name of the registry"
    default: "docker.tangerie.xyz"
    required: false
    type: string
ref:
  description: "branch"
  default: ""
  required: true
  type: string
path:
  default: "."
  required: false
  type: string
```

**Example**
```yml
build-api:
  uses: TangerieOrg/Workflows/.github/workflows/docker-build-push.yml@main
  with:
    image_name: everything-codex-api
    registry_name: docker.tangerie.xyz
    ref: main
    path: api
  secrets: inherit
```

### Deploy
`TangerieOrg/Workflows/.github/workflows/docker-deploy.yml@main`

**Inputs**
```yml
image_name:
  description: "The base name of the image (not including tags or registry)"
  default: "ERROR"
  required: true
  type: string
registry_name:
  description: "The name of the registry"
  default: "docker.tangerie.xyz"
  required: false
  type: string
compose_file_path:
  description: "Path of compose file"
  default: "docker-compose.yml"
  required: false
  type: string
```

**Examples**
```yml
deploy:
  uses: TangerieOrg/Workflows/.github/workflows/docker-deploy.yml@main
  needs: 
    - build-api
    - build-frontend
  with:
    image_name: everything-codex
    registry_name: docker.tangerie.xyz
  secrets: inherit
```