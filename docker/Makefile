OPEN ?= 0
docker-up: ## Start the frontend container
	# OPEN arg is 1 open firefox developer edition
	@if [ "$(OPEN)" -eq "1" ]; then \
		open -a "Firefox Developer Edition" http://localhost:5173; \
	fi
	docker compose up --remove-orphans frontend

docker-run-fish: ## Run a fish shell in a new frontend container
	docker compose run --rm --service-ports --entrypoint fish frontend

docker-exec-fish: ## Execute a fish shell in the running frontend container
	docker compose exec --interactive --tty frontend fish

docker-build: ## Build the frontend container
	docker compose build frontend

# Testing and code quality
docker-build-project: ## Build the project inside the frontend container
	docker compose run --rm --remove-orphans --entrypoint sh frontend -lc "pnpm install --frozen-lockfile && pnpm run build"

docker-format-project: ## Run prettier inside the frontend container
	docker compose run --rm --remove-orphans --entrypoint sh frontend -lc "pnpm install --frozen-lockfile && pnpm exec prettier --write ."

docker-type-check-project: ## Run vue-tsc in the frontend container
	docker compose run --rm --remove-orphans --entrypoint sh frontend -lc "pnpm install --frozen-lockfile && pnpm run type-check"

docker-lint-project: ## Run eslint in the frontend container
	docker compose run --rm --remove-orphans --entrypoint sh frontend -lc "pnpm install --frozen-lockfile && pnpm run lint"

docker-before-commit:
	docker compose run --rm --remove-orphans --entrypoint sh frontend -lc "pnpm install --frozen-lockfile && pnpm run lint && pnpm run type-check && pnpm run build-only"
