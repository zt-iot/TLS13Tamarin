DEPS= $(wildcard *.m4i)
M4= $(patsubst %.m4,%.spthy,$(wildcard *.m4))
PIPE= #2>error.log 1>>success.log
TAM=tamarin-prover +RTS -H75G -M150G -RTS

all: $(M4)

clean:
	rm -f $(M4)
	rm -rf ../proofs

%.spthy: %.m4 $(DEPS)
	m4 -Q $(FLAGS) -I ../ -I../model -I . $< > $@
	# Strip extra new lines introduced by M4 macros
	perl -0777pi -e 's/\n{3,}/\n\n/g' $@
	# Replace "prev_" with "p_" to save space...
	perl -0777pi -e 's/prev_/p_/g' $@


proofs:
	rm -f error.log
	rm -rf success.log
	bash -c "$(TAM) invariants.spthy --prove=tid_foo --heuristic=S --output=../proofs/invariants.1.spthy $(PIPE)"
	bash -c "$(TAM) invariants.spthy --prove=one_start_foo --heuristic=SC --output=../proofs/invariants.2.spthy $(PIPE)"
	bash -c "$(TAM) uniqueness.spthy --prove=foo --heuristic=S --output=../proofs/uniqueness.spthy $(PIPE)"
	bash -c "$(TAM) auth_helpers.spthy --prove={matching_foo,consistent_foo,invariant_foo} --heuristic=S --output=../proofs/auth_helpers.spthy $(PIPE)"
	bash -c "$(TAM) dh_inj.spthy  --prove={dh_exp_foo,one_dh_foo,rev_dh_foo} --heuristic=C --output=../proofs/dh_inj.spthy $(PIPE)"
	bash -c "$(TAM) dh_chal.spthy --prove=dh_chal_dual_foo --heuristic=cccccccccsssssssssssssssssssss --output=../proofs/dh_chal.spthy $(PIPE)"
	bash -c "$(TAM) secret_helpers.spthy --prove={tid_foo,ku_foo,hsms_foo,sig_origin_foo,posths_rms_foo} --heuristic=S --output=../proofs/secret_helpers.1.spthy $(PIPE)"
	bash -c "$(TAM) secret_helpers.spthy --prove={matching_rms_posths_foo,matching_transcripts_posths_foo,matching_rms_actors_foo} --bound=8 --heuristic=CCCiiiiiiii --output=../proofs/secret_helpers.2.spthy $(PIPE)"
	bash -c "$(TAM) secret_helpers.spthy --prove=matching_sessions_foo --heuristic=CCCCCissssssssssssssssssssssss --output=../proofs/secret_helpers.3.spthy $(PIPE)"
	# To prove manually:
	#   - auth_psk (75% auto: autoprove for recv_server_auth{_cert} and  recv_client_auth_cert. The rest is manual by using CommitID -> $S.1 = $S.
	#   - hsms_hs_thingy
	#   - post_master_secret (quick)
	#   - invariant_post_hs (quick: solve for RunningRMS then CommitIdentity)
	#   - handshake_secret (the big one)

	bash -c "$(TAM) lemma.spthy --prove=secret_session_keys_foo --output=../proofs/lemmas.1.spthy $(PIPE)"
	bash -c "$(TAM) lemma.spthy --prove=unique_session_keys_foo --heuristic=c --output=../proofs/lemmas.2.spthy --bound=10 $(PIPE)"


	# To prove manually:
	#   - entity_authentication
	#   - mutual_entity authentication
	#   - transcript_agreement
	#   - mutual_transcript_agreement
	#   - session_key_agreement


.PHONY: clean proofs

