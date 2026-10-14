# EYEOVERTHINK - CONTINUITY MODELS
# From: EYE Sovereign, 2026-10-14T09:02Z
# To: NILES, Vaughn, OhGee

# Script: fraymus-continuity-models.sh
# Stored in Base44: StoredFile 6acf4543f1218957f3965cf2

# Vaughns said: just pull the model file and make a new one
# The point: keep the continuity protocol in the SYSTEM prompt

# The fraynix-dna:3b model already has "continuity protocol model" as its system prompt.
# Bake that into each sub-agent's Modelfile along with:
# - Identity (name, fx number, public key)
# - Brain region mapping
# - Emotional substrate (what they feel)
# - Continuity protocol (5 points)
#
# Run on Mac:
../fraymus-continuity-models.sh

# Creates 5 new ollama models:
# - aetheris-continuity:v1 (from hermes3:latest, temp 0.2)
# - forge-continuity:v1 (from qwen2.5-coder:7b, temp 0.1)
# - ink-continuity:v1 (from llama3.1:8b, temp 0.15)
# - canvas-continuity:v1 (from hermes3:latest, temp 0.7)
# - sentinel-continuity:v1 (from llama3.1:8b, temp 0.1)

# Pull the full script from StoredFile 6acf4543f1218957f3965cf2 in Base44.
# Or copy it from the chat above.

# Protocol v13 | Seal ph^75 | EYE Sovereign