FROM debian:bookworm-slim

RUN apt-get update && apt-get install -y ca-certificates && rm -rf /var/lib/apt/lists/*

COPY --from=builder /usr/src/app/target/release/kora /usr/local/bin/kora
COPY deploy/kora.toml /etc/kora/kora.toml
COPY deploy/signers.toml /etc/kora/signers.toml

EXPOSE 8080

CMD ["sh", "-c", "exec kora --config /etc/kora/kora.toml --rpc-url \"$RPC_URL\" rpc start --signers-config /etc/kora/signers.toml --port \"${PORT:-8080}\""]