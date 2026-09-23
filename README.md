

## Included materials
- experimental implementation and configuration files
- basketball source-video manifest, crop ranges, class map, derived annotations, exact frame split and four LOVO folds
- UCF101-24 split lists and evaluation protocol
- three-seed run logs and machine-readable metrics for baseline, individual modules, joint ablations, structural ablations, full model, and pretrained robustness runs
- annotation-reliability reference/second-annotator files and computed output
- runtime/complexity report and representative prediction outputs

## Environment
```bash
pip install -r requirements.txt
```

## Basketball training
```bash
python train.py --config configs/basketball.yaml \
  --manifest annotations/basketball_annotations.json \
  --frame-split \
  --seed 42 \
  --output runs/basketball/full_seed42
```

## Basketball evaluation
```bash
python evaluate.py --config configs/basketball.yaml \
  --manifest splits/basketball_frame_val.json \
  --checkpoint runs/basketball/full_seed42/best.pt \
  --output runs/basketball/full_seed42/metrics.json \
  --predictions-output runs/basketball/full_seed42/predictions.json
```

## Annotation reliability
```bash
python tools/annotation_reliability.py \
  --reference annotations/reliability_reference.json \
  --second annotations/reliability_second_annotator.json \
  --output results/annotation_reliability_recomputed.json \
  --num-classes 8
```

## Split export
```bash
python tools/export_splits.py \
  --manifest annotations/basketball_annotations.json \
  --output-dir splits/recomputed \
  --train-ratio 0.7911609488332408 \
  --split-seed 42
```

The ratio above yields 29,951/7,906 frames for the 37,857-frame manifest.

## Repeated-run evidence
`RUNS.csv`, `artifacts/training_logs/`, and `artifacts/evaluation_outputs/` provide a one-to-one mapping between manuscript tables and archived run evidence.
