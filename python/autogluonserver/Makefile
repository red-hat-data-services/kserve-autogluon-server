RUFF_CFG := ../../ruff.toml

dev_install:
	uv sync --active --group test

install_dependencies:
	uv sync --active --group test
	
test: type_check
	pytest -W ignore

type_check:
	mypy --ignore-missing-imports autogluonserver

# Fast single-file checks (after `uv sync --active --group test`). No full-tree ruff/mypy.
# Usage: make lint-file FILE=autogluonserver/tabular_model.py
.PHONY: lint-file format-file typecheck-file
lint-file:
	@if [ -z "$(FILE)" ]; then echo 'Usage: make lint-file FILE=autogluonserver/path.py'; exit 1; fi
	uvx ruff check --config $(RUFF_CFG) $(FILE)

format-file:
	@if [ -z "$(FILE)" ]; then echo 'Usage: make format-file FILE=autogluonserver/path.py'; exit 1; fi
	uvx ruff format --config $(RUFF_CFG) $(FILE)

typecheck-file:
	@if [ -z "$(FILE)" ]; then echo 'Usage: make typecheck-file FILE=autogluonserver/path.py'; exit 1; fi
	mypy --ignore-missing-imports $(FILE)
