# 2-floor-computer-pass-info

GC_token='eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6InlnMjQzN0BueXUuZWR1IiwibGV2ZWwiOiJub2F1dGgiLCJpbWFnZS11cmwiOiJodHRwczovL2xoMy5nb29nbGV1c2VyY29udGVudC5jb20vYS9BQ2c4b2NKM0NHTHQ4V0VvcE1Dc3RLOTdTajJTUkROWk5OR2ZPVlB4Z0RiQzZ6NlZ3RUtsRVVzPXM5Ni1jP3N6PTUwP3N6PTUwIiwiZXhwIjoxOTY2OTU2MzI3fQ.0hkA3sx3ZtXEooxUwb0YMrXsRH-TE94zQXepr2qo9ok'

from neuprint import Client, fetch_synapse_connections

c = Client('neuprint.janelia.org',
           dataset='hemibrain:v1.2.1',
           token= GC_token)

pairs = [
    (846991524, 910447220),
    (1225640135, 846991524),
]

for pre_id, post_id in pairs:
    print(f"\n=== {pre_id} -> {post_id} ===")
    conn_df = fetch_synapse_connections(
        source_criteria=pre_id,
        target_criteria=post_id,
        nt='max',
        client=c          # <-- explicitly tell it which client to use
    )
    print(conn_df[['bodyId_pre', 'bodyId_post', 'x_pre', 'y_pre', 'z_pre', 'nt', 'ntProb']])
    print(conn_df['nt'].value_counts())





